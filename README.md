# Armis AppSec - SBOM & Supply Chain Lab Repository

Training repository for Armis Centrix for AppSec supply chain security labs. Contains realistic lockfiles, SBOMs, and vulnerable dependency scenarios for use in hands-on labs.

## Repository Structure

```
armis-appsec-sbom/
├── README.md (this file)
├── .gitignore
├── lab-2.1-basic-sboms/
│   ├── simple-web-app.cyclonedx.json
│   ├── simple-web-app.cyclonedx.xml
│   └── README.md
├── lab-2.2-lockfiles/
│   ├── npm-project/
│   │   ├── package.json
│   │   └── package-lock.json
│   ├── python-project/
│   │   ├── requirements.txt
│   │   └── poetry.lock
│   ├── ruby-project/
│   │   ├── Gemfile
│   │   └── Gemfile.lock
│   ├── go-project/
│   │   ├── go.mod
│   │   └── go.sum
│   └── README.md
├── lab-2.3-dependency-gating/
│   ├── gating-policy.json
│   ├── complex-app-sbom.cyclonedx.json
│   └── README.md
├── lab-2.4-supply-chain-attacks/
│   ├── typosquatting-scenario.json
│   ├── compromised-dep-scenario.json
│   └── README.md
└── lab-2.5-artifact-signing/
    ├── signed-sbom.cyclonedx.json
    ├── signature.sig
    └── README.md
```

## Lab Coverage

- **Lab 2.1**: SBOM Analysis & Vulnerability Mapping - Basic CycloneDX format, simple dependencies
- **Lab 2.2**: Lockfile Auditing - npm, Python, Ruby, Go with known CVEs
- **Lab 2.3**: Dependency Gating & Policy - Policy enforcement scenarios
- **Lab 2.4**: Supply Chain Attacks - Typosquatting and compromise detection
- **Lab 2.5**: Artifact Signing & Verification - Signed SBOMs and signatures

## Known Vulnerabilities Included

All dependencies are intentionally outdated to demonstrate vulnerability detection:

- **npm:** express 4.16.2, lodash 4.17.4, request 2.87.0
- **Python:** flask 0.12.3, jinja2 2.9.0, requests 2.20.0
- **Ruby:** rails 5.0.0, nokogiri 1.8.0
- **Go:** github.com/dgrijalva/jwt-go v3.2.0

**For Training Use Only** - Do not use in production environments.

## Quick Start

Clone the repo:

```
git clone https://github.com/achild-armis/armis-appsec-sbom.git
cd armis-appsec-sbom
```

List all files:

```
find . -type f -name "*.json" -o -name "*.lock" -o -name "*.txt"
```

## File Formats

- **CycloneDX JSON** - Machine-readable SBOM format (preferred)
- **CycloneDX XML** - Alternative SBOM format
- **Lockfiles** - Native package manager lockfiles (package-lock.json, poetry.lock, etc.)
- **JSON Policy Files** - Dependency gating policies

## Usage in Labs

Each lab subdirectory includes a README with specific commands and exercises. Start with Lab 2.1 and progress sequentially.

Example:

```
cd lab-2.1-basic-sboms
cat simple-web-app.cyclonedx.json
armis-cli scan sbom simple-web-app.cyclonedx.json --output findings.txt
```

## Contributing

For ServiceNow AppSec team use. To add new scenarios:

1. Create a new subdirectory under the appropriate lab folder
2. Include a README explaining the scenario
3. Add realistic lockfiles or SBOMs
4. Document known vulnerabilities

## Support

For questions, contact the Armis AppSec team or your ServiceNow AppSec CoE.

---

**Last Updated:** October 2026
**Version:** 1.0 (Labs 2.1-2.5)
