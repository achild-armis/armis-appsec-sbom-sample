# Armis AppSec SBOM Repository - Upload Instructions

This document explains how to organize and upload the generated files to create the `armis-appsec-sbom` GitHub repository.

## Files Generated

All files are in `/mnt/user-data/outputs/` with prefixes indicating their destination:

### Root Level

- `armis-appsec-sbom-README.md` → Rename to `README.md`
- `armis-appsec-sbom-.gitignore` → Rename to `.gitignore`

### Lab 2.1 - Basic SBOMs

Create directory: `lab-2.1-basic-sboms/`

Files to place inside:
- `lab-2.1-basic-sboms-README.md` → `README.md`
- `lab-2.1-simple-web-app.cyclonedx.json` → `simple-web-app.cyclonedx.json`
- `lab-2.1-simple-web-app.cyclonedx.xml` → `simple-web-app.cyclonedx.xml`

### Lab 2.2 - Lockfiles

Create directory structure:

```
lab-2.2-lockfiles/
├── README.md
├── npm-project/
│   ├── package.json
│   └── package-lock.json
├── python-project/
│   ├── requirements.txt
│   └── poetry.lock
├── ruby-project/
│   ├── Gemfile
│   └── Gemfile.lock
└── go-project/
    ├── go.mod
    └── go.sum
```

Files to place:
- `lab-2.2-lockfiles-README.md` → `lab-2.2-lockfiles/README.md`
- `lab-2.2-npm-package.json` → `lab-2.2-lockfiles/npm-project/package.json`
- `lab-2.2-npm-package-lock.json` → `lab-2.2-lockfiles/npm-project/package-lock.json`
- `lab-2.2-python-requirements.txt` → `lab-2.2-lockfiles/python-project/requirements.txt`
- `lab-2.2-python-poetry.lock` → `lab-2.2-lockfiles/python-project/poetry.lock`
- `lab-2.2-ruby-Gemfile` → `lab-2.2-lockfiles/ruby-project/Gemfile`
- `lab-2.2-ruby-Gemfile.lock` → `lab-2.2-lockfiles/ruby-project/Gemfile.lock`
- `lab-2.2-go-go.mod` → `lab-2.2-lockfiles/go-project/go.mod`
- `lab-2.2-go-go.sum` → `lab-2.2-lockfiles/go-project/go.sum`

## Step-by-Step Upload

### 1. Create GitHub Repository

```
Repository name: armis-appsec-sbom
Description: Training repository for Armis AppSec supply chain security labs
Visibility: Public (or Private, per your preference)
Initialize with README: No (we'll add ours)
```

### 2. Clone the Repository Locally

```bash
git clone https://github.com/achild-armis/armis-appsec-sbom.git
cd armis-appsec-sbom
```

### 3. Create Directory Structure

```bash
mkdir -p lab-2.1-basic-sboms
mkdir -p lab-2.2-lockfiles/npm-project
mkdir -p lab-2.2-lockfiles/python-project
mkdir -p lab-2.2-lockfiles/ruby-project
mkdir -p lab-2.2-lockfiles/go-project
```

### 4. Copy Root Files

From `/mnt/user-data/outputs/`:

```bash
cp armis-appsec-sbom-README.md README.md
cp armis-appsec-sbom-.gitignore .gitignore
```

### 5. Copy Lab 2.1 Files

```bash
cp lab-2.1-basic-sboms-README.md lab-2.1-basic-sboms/README.md
cp lab-2.1-simple-web-app.cyclonedx.json lab-2.1-basic-sboms/
cp lab-2.1-simple-web-app.cyclonedx.xml lab-2.1-basic-sboms/
```

### 6. Copy Lab 2.2 Files

```bash
cp lab-2.2-lockfiles-README.md lab-2.2-lockfiles/README.md

# npm
cp lab-2.2-npm-package.json lab-2.2-lockfiles/npm-project/package.json
cp lab-2.2-npm-package-lock.json lab-2.2-lockfiles/npm-project/package-lock.json

# Python
cp lab-2.2-python-requirements.txt lab-2.2-lockfiles/python-project/requirements.txt
cp lab-2.2-python-poetry.lock lab-2.2-lockfiles/python-project/poetry.lock

# Ruby
cp lab-2.2-ruby-Gemfile lab-2.2-lockfiles/ruby-project/Gemfile
cp lab-2.2-ruby-Gemfile.lock lab-2.2-lockfiles/ruby-project/Gemfile.lock

# Go
cp lab-2.2-go-go.mod lab-2.2-lockfiles/go-project/go.mod
cp lab-2.2-go-go.sum lab-2.2-lockfiles/go-project/go.sum
```

### 7. Verify Directory Structure

```bash
tree -L 3
# Should show:
# .
# ├── README.md
# ├── .gitignore
# ├── lab-2.1-basic-sboms/
# │   ├── README.md
# │   ├── simple-web-app.cyclonedx.json
# │   └── simple-web-app.cyclonedx.xml
# └── lab-2.2-lockfiles/
#     ├── README.md
#     ├── npm-project/
#     ├── python-project/
#     ├── ruby-project/
#     └── go-project/
```

### 8. Commit and Push

```bash
git add -A
git commit -m "Initial commit: Labs 2.1-2.2 with basic SBOMs and lockfiles"
git push origin main
```

## Verification

After pushing, verify the repository structure on GitHub:

1. Navigate to `https://github.com/achild-armis/armis-appsec-sbom`
2. Verify directory structure matches above
3. Check that all README files are readable
4. Spot-check that lockfiles are properly formatted

## Next Steps

Once the repository is live:

1. Update the main LABS_INDEX.md to reference this new repo
2. Share the link with training participants
3. Begin building Lab 2.3-2.5 with same structure

## File Manifest

Total files generated: 11

- 1 x README (repo root)
- 1 x .gitignore
- 1 x Lab 2.1 README
- 2 x SBOM files (JSON + XML)
- 1 x Lab 2.2 README
- 8 x Lockfiles (npm, Python, Ruby, Go × 2)

---

**Generated:** October 1, 2026
**For:** Armis Centrix for AppSec Training Curriculum
**Version:** 1.0 (Labs 2.1-2.2)
