# Lab 2.2 - Lockfile Auditing

Audit native package manager lockfiles for known vulnerabilities. Learn how different package managers represent dependencies and how Armis scans them.

## Prerequisites

- Lab 2.1 complete
- armis-cli 1.1.0+
- API credentials configured

## What You'll Learn

- Lockfile formats (package-lock.json, poetry.lock, Gemfile.lock, go.sum)
- Transitive dependency vulnerabilities
- Package manager differences
- Version pinning and reproducibility
- Supply chain attack vectors

## Files in This Lab

### npm Project

- `npm-project/package.json` - npm manifest with direct dependencies
- `npm-project/package-lock.json` - npm lockfile with full dependency tree

### Python Project

- `python-project/requirements.txt` - pip requirements (flat list)
- `python-project/poetry.lock` - Poetry lockfile (locked versions)

### Ruby Project

- `ruby-project/Gemfile` - Ruby manifest with dependencies
- `ruby-project/Gemfile.lock` - Bundler lockfile (locked versions)

### Go Project

- `go-project/go.mod` - Go module manifest
- `go-project/go.sum` - Go module checksums (not a lockfile, but used for verification)

## Part 1: Examine Lockfile Formats

### npm

View package.json:

```
cat npm-project/package.json
```

Observe direct dependencies declared.

View package-lock.json structure:

```
cat npm-project/package-lock.json | head -50
```

Observe:
- Each package has version, integrity hash
- Nested dependencies tree
- Lockfile is deterministic (same hash for reproducible installs)

### Python

View requirements.txt:

```
cat python-project/requirements.txt
```

Simple format - one package per line with version.

View poetry.lock:

```
cat python-project/poetry.lock | head -50
```

Observe:
- [[package]] sections for each package
- Files hash for integrity
- Dependencies nested under each package

### Ruby

View Gemfile:

```
cat ruby-project/Gemfile
```

Declare gem dependencies with version constraints.

View Gemfile.lock:

```
cat ruby-project/Gemfile.lock | head -50
```

Observe:
- Locked versions (PLATFORM, GEM sections)
- Dependencies listed under each gem

### Go

View go.mod:

```
cat go-project/go.mod
```

Module dependencies with semantic versioning.

View go.sum:

```
cat go-project/go.sum | head -20
```

Observe:
- Module name, version, hash pairs
- Used to verify module integrity (not for version pinning)

## Part 2: Scan Individual Lockfiles

Scan npm lockfile (if armis-cli supports it):

```
cd npm-project
armis-cli scan sbom package-lock.json --output npm-findings.txt
```

Or generate SBOM from lockfile, then scan:

```
# Alternative: tools like cyclonedx-npm can convert
cd ..
```

Scan Python poetry.lock:

```
cd python-project
cat poetry.lock | head -20
```

Scan Ruby Gemfile.lock:

```
cd ruby-project
cat Gemfile.lock | head -20
```

Scan Go go.sum:

```
cd go-project
cat go.sum | head -10
```

## Part 3: Analyze Transitive Dependencies

View npm transitive dependencies:

```
cd npm-project
cat package-lock.json | grep -A5 "dependencies"
```

Count unique packages (direct + transitive):

```
cat package-lock.json | grep '"name"' | wc -l
```

Compare to package.json:

```
cat package.json | grep -c '":' 
```

Observe: lockfile includes many more packages (transitive deps).

## Part 4: Identify Vulnerable Versions

Look for outdated packages in each lockfile:

npm:

```
grep -i "4.16.2\|4.17.4\|2.87.0" npm-project/package-lock.json
```

Python:

```
grep -i "flask\|jinja2\|requests" python-project/poetry.lock | head -10
```

Ruby:

```
grep -i "rails\|nokogiri" ruby-project/Gemfile.lock | head -10
```

## Part 5: Compare Package Manager Approaches

Create a comparison table mentally:

| Package Manager | Lockfile | Hash/Checksum | Version Constraint | Transitive Deps |
|---|---|---|---|---|
| npm | package-lock.json | integrity (SHA) | Exact | Nested |
| Python Poetry | poetry.lock | sha256 | Exact | Listed |
| Ruby Bundler | Gemfile.lock | - | Exact | Listed |
| Go | go.sum | hash (h1) | Versioned | In go.mod |

## Key Concepts

**Lockfile** - Exact record of all dependencies (direct + transitive) used in a build, ensuring reproducibility.

**Transitive Dependency** - A dependency of a dependency. Often overlooked but can introduce vulnerabilities.

**Version Pinning** - Locking to exact version instead of ranges (e.g., 1.2.3 vs ~1.2.0).

**Integrity Hash** - Cryptographic hash verifying package contents haven't been tampered with.

## Troubleshooting

**"armis-cli scan sbom" doesn't work with lockfiles?**

Some package managers require conversion to CycloneDX SBOM first. Tools like:
- cyclonedx-npm (npm → CycloneDX)
- cyclonedx-python (Python → CycloneDX)
- cyclonedx-gradle (Ruby → CycloneDX)

Lab 2.3 covers policy-based scanning.

**Lockfile shows versions, but no vulnerabilities?**

Vulnerability detection happens server-side against NVD. Allow 30-60 seconds for processing.

## Lab Complete

You now understand:
- Different lockfile formats across package managers
- How transitive dependencies increase surface area
- Why lockfiles are critical for reproducibility
- How to examine and compare lockfiles

## Next Lab

Proceed to Lab 2.3: Dependency Gating and Policy Enforcement to implement security policies.
