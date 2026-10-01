# Lab 2.4 - Supply Chain Attacks

Learn to detect and respond to supply chain attack patterns including typosquatting, dependency hijacking, and compromised packages.

## Prerequisites

- Lab 2.1-2.3 complete
- armis-cli 1.1.0+
- Understanding of package registries (npm, PyPI, etc.)
- API credentials configured

## What You'll Learn

- Typosquatting attack patterns
- Compromised dependency detection
- Package registry impersonation
- Malicious transitive dependencies
- Attack tree analysis
- Incident response workflow

## Files in This Lab

- `typosquatting-scenario.json` - Common misspellings targeting developers
- `compromised-dep-scenario.json` - Real-world hijacking scenarios
- `README.md` (this file)

## Part 1: Understand Typosquatting

Typosquatting exploits developer mistakes when typing package names. View scenarios:

```
cat typosquatting-scenario.json | jq .
```

Common patterns:
- `expres` instead of `express` (missing letter)
- `react-dom-` instead of `react-dom` (extra character)
- `lodsh` instead of `lodash` (transposition)
- `momnet` instead of `moment` (vowel swap)

Each malicious package appears legitimate but contains:
- Credential stealers
- Cryptominers
- Backdoors
- Dependency chain infection

## Part 2: Detection Strategies

**Exact match verification:**

Check package names against known registry:

```bash
npm search express (official)
npm search expres (typo - would return malicious package)
```

**Levenshtein distance analysis:**

Packages differing by 1-2 characters from popular packages are suspicious.

**Checksum verification:**

Verify package integrity against known good checksums.

**Registry reputation:**

Official registry > community packages. Know your sources.

## Part 3: Compromised Dependency Detection

View hijacked scenarios:

```
cat compromised-dep-scenario.json | jq .
```

Scenarios covered:
1. Version hijacking - Old package version taken over, malicious code injected
2. Maintainer account compromise - Attacker gains npm account, releases bad version
3. Subdependency infection - Attack hides in rarely-audited transitive dependency
4. Build-time injection - Malicious code in postinstall scripts
5. Metadata spoofing - Fake author, misleading description

## Part 4: Attack Trees

Map attack flows:

**Typosquatting Attack Tree:**
```
Typosquatting
├─ Developer Types Wrong Name
│  └─ Installs Malicious Package
│     ├─ Runs postinstall Script
│     │  ├─ Steals env vars (API keys, tokens)
│     │  ├─ Injects Backdoor
│     │  └─ Exfiltrates Source Code
│     └─ Compromises Build Pipeline
├─ CI/CD Pipeline Injection
│  └─ Propagates to Production
└─ Lateral Movement in Org
```

## Part 5: Detection with armis-cli

Scan for suspicious patterns:

```bash
armis-cli scan repo . --format json | grep -E "typo|confusable|name-similarity"
```

## Part 6: Response Workflow

**If compromised package detected:**

1. Stop - Halt all installations immediately
2. Assess - Identify which versions are malicious
3. Inventory - List all affected services/builds
4. Isolate - Remove credentials, rotate tokens
5. Remediate - Update to patched version
6. Verify - Run security scans on affected builds
7. Communicate - Notify affected teams
8. Monitor - Watch for lateral movement

## Part 7: Prevention Strategies

**Developer Level:**
- Copy-paste package names (don't type)
- Verify package in registry before install
- Pin exact versions in lockfiles
- Regular npm audit runs

**Organization Level:**
- Private registry mirror
- Package allowlist/blocklist
- Automated scanning in CI/CD
- Security notifications for high-profile packages

**Pipeline Level:**
- Signed commits and builds
- Immutable artifact storage
- SBOM generation on every build
- Policy enforcement on dependencies

## Key Concepts

**Typosquatting** - Registering domain/package names similar to popular ones.

**Hijacking** - Taking control of a legitimate package (account compromise).

**Postinstall script** - Code that runs during package installation (high-risk vector).

**Transitive dependency** - A dependency of a dependency; harder to audit.

**Attestation** - Cryptographic proof of package authenticity.

## Lab Complete

You now understand:
- Typosquatting attack patterns
- Compromised dependency detection
- Attack tree analysis
- Supply chain risk assessment
- Incident response workflows
- Prevention strategies

## Next Lab

Proceed to Lab 2.5: Artifact Signing & Verification for cryptographic integrity.
