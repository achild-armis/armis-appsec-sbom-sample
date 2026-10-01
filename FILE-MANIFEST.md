# Armis AppSec SBOM Repository - Complete File Manifest

**Generated:** October 1, 2026  
**Version:** 1.0 (Labs 2.1-2.5 Prep)  
**Total Files:** 13  

All files are ready in `/mnt/user-data/outputs/` for upload to GitHub.

---

## Root Repository Files

### 1. `armis-appsec-sbom-README.md`
**Purpose:** Repository root README  
**Destination:** Rename to `README.md` in repo root  
**Size:** ~2KB  
**Content:** Repository overview, structure, lab coverage, quick start, usage  
**Status:** ✅ Complete

### 2. `armis-appsec-sbom-.gitignore`
**Purpose:** Git ignore file  
**Destination:** Rename to `.gitignore` in repo root  
**Size:** ~1KB  
**Content:** Node modules, Python cache, IDEs, lab outputs, credentials  
**Status:** ✅ Complete

---

## Lab 2.1 - SBOM Analysis & Vulnerability Mapping

### 3. `lab-2.1-basic-sboms-README.md`
**Purpose:** Lab instructions and learning objectives  
**Destination:** `lab-2.1-basic-sboms/README.md`  
**Size:** ~4KB  
**Content:** 5-part lab structure, SBOM format basics, hands-on exercises, troubleshooting  
**Topics Covered:**
- SBOM structure (metadata, components, vulnerabilities)
- Component identification and versioning
- CVE mapping and NVD lookup
- Multiple output formats (JSON, SARIF)
**Status:** ✅ Complete

### 4. `lab-2.1-simple-web-app.cyclonedx.json`
**Purpose:** Sample SBOM in JSON format  
**Destination:** `lab-2.1-basic-sboms/simple-web-app.cyclonedx.json`  
**Size:** ~5KB  
**Content:** 8 components with 6 known CVEs  
**Components:**
- express 4.16.2 (CVE-2018-3710)
- lodash 4.17.4 (CVE-2019-10744 - CRITICAL)
- request 2.87.0 (CVE-2017-16168)
- qs 6.5.1 (CVE-2017-1000381)
- moment 2.20.1 (CVE-2022-24999)
- xml2js 0.4.19 (CVE-2014-4940)
- mongoose 5.0.1
- debug 3.1.0
**Status:** ✅ Complete

### 5. `lab-2.1-simple-web-app.cyclonedx.xml`
**Purpose:** Same SBOM in XML format  
**Destination:** `lab-2.1-basic-sboms/simple-web-app.cyclonedx.xml`  
**Size:** ~4KB  
**Content:** Identical to JSON SBOM, different format  
**Status:** ✅ Complete

---

## Lab 2.2 - Lockfile Auditing

### 6. `lab-2.2-lockfiles-README.md`
**Purpose:** Lab instructions for lockfile auditing  
**Destination:** `lab-2.2-lockfiles/README.md`  
**Size:** ~4KB  
**Content:** 5-part lab structure, lockfile format comparison, hands-on exercises  
**Topics Covered:**
- npm, Python, Ruby, Go lockfile formats
- Transitive dependency trees
- Version pinning and reproducibility
- Supply chain attack vectors
- Lockfile analysis techniques
**Status:** ✅ Complete

### 7. `lab-2.2-npm-package.json`
**Purpose:** npm project manifest  
**Destination:** `lab-2.2-lockfiles/npm-project/package.json`  
**Size:** ~1KB  
**Content:** 8 dependencies + 2 dev dependencies  
**Status:** ✅ Complete

### 8. `lab-2.2-npm-package-lock.json`
**Purpose:** npm lockfile with dependency tree  
**Destination:** `lab-2.2-lockfiles/npm-project/package-lock.json`  
**Size:** ~3KB  
**Content:** Locked versions with integrity hashes, full transitive tree  
**Packages:** 40+ (direct + transitive)  
**Status:** ✅ Complete

### 9. `lab-2.2-python-requirements.txt`
**Purpose:** Python pip requirements  
**Destination:** `lab-2.2-lockfiles/python-project/requirements.txt`  
**Size:** ~0.3KB  
**Content:** 5 Python packages with exact versions  
**Status:** ✅ Complete

### 10. `lab-2.2-python-poetry.lock`
**Purpose:** Python Poetry lockfile  
**Destination:** `lab-2.2-lockfiles/python-project/poetry.lock`  
**Size:** ~2KB  
**Content:** 11 packages with lockfile metadata and transitive deps  
**Status:** ✅ Complete

### 11. `lab-2.2-ruby-Gemfile`
**Purpose:** Ruby Gemfile manifest  
**Destination:** `lab-2.2-lockfiles/ruby-project/Gemfile`  
**Size:** ~0.8KB  
**Content:** 15 gems with exact versions  
**Status:** ✅ Complete

### 12. `lab-2.2-ruby-Gemfile.lock`
**Purpose:** Ruby Bundler lockfile  
**Destination:** `lab-2.2-lockfiles/ruby-project/Gemfile.lock`  
**Size:** ~8KB  
**Content:** 76 gem entries with dependency tree  
**Status:** ✅ Complete

### 13. `lab-2.2-go-go.mod`
**Purpose:** Go module manifest  
**Destination:** `lab-2.2-lockfiles/go-project/go.mod`  
**Size:** ~0.3KB  
**Content:** 4 Go modules with versions  
**Status:** ✅ Complete

### 14. `lab-2.2-go-go.sum`
**Purpose:** Go module checksums  
**Destination:** `lab-2.2-lockfiles/go-project/go.sum`  
**Size:** ~1KB  
**Content:** 9 module hashes for integrity verification  
**Status:** ✅ Complete

---

## Lab 2.3+ Preview Files

### 15. `lab-2.3-gating-policy.json`
**Purpose:** Sample dependency gating policy  
**Destination:** `lab-2.3-dependency-gating/gating-policy.json` (pending)  
**Size:** ~2KB  
**Content:** 6 security rules, exceptions, whitelist, report thresholds  
**Rules Include:**
- Fail on CRITICAL vulnerabilities
- Warn on HIGH (max 5)
- Block copyleft licenses
- Flag deprecated packages
- Review >2 year old packages
- Transitive depth limits
**Status:** ✅ Complete

---

## Support Documentation

### 16. `SBOM-REPO-UPLOAD-INSTRUCTIONS.md`
**Purpose:** Step-by-step guide for GitHub upload  
**Location:** Keep in outputs, reference for manual upload  
**Size:** ~2KB  
**Content:** Directory structure, file mapping, Git commands  
**Status:** ✅ Complete

### 17. `FILE-MANIFEST.md`
**Purpose:** This file - complete inventory  
**Location:** Reference only  
**Size:** ~4KB  
**Status:** ✅ Complete

---

## Directory Structure (When Uploaded)

```
armis-appsec-sbom/
├── README.md (from #1)
├── .gitignore (from #2)
├── lab-2.1-basic-sboms/
│   ├── README.md (from #3)
│   ├── simple-web-app.cyclonedx.json (from #4)
│   └── simple-web-app.cyclonedx.xml (from #5)
├── lab-2.2-lockfiles/
│   ├── README.md (from #6)
│   ├── npm-project/
│   │   ├── package.json (from #7)
│   │   └── package-lock.json (from #8)
│   ├── python-project/
│   │   ├── requirements.txt (from #9)
│   │   └── poetry.lock (from #10)
│   ├── ruby-project/
│   │   ├── Gemfile (from #11)
│   │   └── Gemfile.lock (from #12)
│   └── go-project/
│       ├── go.mod (from #13)
│       └── go.sum (from #14)
└── lab-2.3-dependency-gating/ (placeholder for future)
    └── gating-policy.json (from #15)
```

---

## Known Vulnerabilities Included (Training Only)

All packages contain intentional, known CVEs for learning purposes:

### npm / Node.js
- **express 4.16.2**: CVE-2018-3710 (Open Redirect)
- **lodash 4.17.4**: CVE-2019-10744 (Prototype Pollution - CRITICAL)
- **request 2.87.0**: CVE-2017-16168 (SSRF)
- **qs 6.5.1**: CVE-2017-1000381 (Prototype Pollution)
- **moment 2.20.1**: CVE-2022-24999 (ReDoS)
- **xml2js 0.4.19**: CVE-2014-4940 (XXE)

### Python
- **flask 0.12.3**: Multiple vulnerabilities
- **jinja2 2.9.0**: Sandbox escape
- **requests 2.20.0**: SSL verification bypass
- **werkzeug 0.12.2**: Debug mode REPL access

### Ruby
- **rails 5.0.0**: Multiple CVEs
- **nokogiri 1.8.0**: XXE and code execution

### Go
- **dgrijalva/jwt-go v3.2.0**: Algorithm substitution attack

---

## Upload Checklist

Before uploading to GitHub:

- [ ] Review SBOM-REPO-UPLOAD-INSTRUCTIONS.md
- [ ] Create GitHub repo: `armis-appsec-sbom`
- [ ] Clone repo locally
- [ ] Create directory structure
- [ ] Copy files to correct locations
- [ ] Rename root README and .gitignore (remove prefix)
- [ ] Verify file structure with `tree -L 3`
- [ ] Commit with message: "Initial commit: Labs 2.1-2.2"
- [ ] Push to origin/main
- [ ] Verify on GitHub.com
- [ ] Update LABS_INDEX.md with repo link

---

## Next Phase (To Build)

The following labs are planned but not yet built:

### Lab 2.3 - Dependency Gating
- Complex SBOM with policy violations
- Policy enforcement scenarios
- CI/CD integration

### Lab 2.4 - Supply Chain Attacks
- Typosquatting scenarios
- Compromised dependency detection
- Attack tree analysis

### Lab 2.5 - Artifact Signing
- Signed SBOM examples
- Signature verification
- Chain of custody

---

## File Statistics

| Metric | Value |
|--------|-------|
| Total Files | 17 |
| Total Size | ~45KB |
| READMEs | 3 |
| SBOMs (JSON/XML) | 2 |
| Lockfiles | 8 |
| Config/Policy | 1 |
| Support Docs | 3 |
| Labs Covered | 2.1, 2.2 (plus 2.3 preview) |

---

## Quality Checklist

✅ All files created successfully  
✅ All READMEs include learning objectives  
✅ All lockfiles use realistic package versions  
✅ All files include known vulnerabilities  
✅ Directory structure matches curriculum  
✅ File naming conventions consistent  
✅ Upload instructions clear and complete  

---

**Generated by:** Armis AppSec Training Curriculum Builder  
**For Organization:** ServiceNow Armis AppSec (Partner)  
**Date:** October 1, 2026  
**Version:** 1.0-labs-2.1-2.2
