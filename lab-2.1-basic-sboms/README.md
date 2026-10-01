# Lab 2.1 - SBOM Analysis & Vulnerability Mapping

Learn how to analyze Software Bill of Materials (SBOM) files and map vulnerabilities to specific components.

## Prerequisites

- Armis CLI 1.1.0+
- API credentials configured
- Lab 0.1-0.2 complete

## What You'll Learn

- SBOM format basics (CycloneDX JSON and XML)
- Component identification and versioning
- Vulnerability mapping to components
- CPE (Common Platform Enumeration) and NVD (National Vulnerability Database) links
- Output analysis and filtering

## Files in This Lab

- `simple-web-app.cyclonedx.json` - Basic SBOM in JSON format
- `simple-web-app.cyclonedx.xml` - Same SBOM in XML format

## Part 1: Examine SBOM Structure

View the JSON SBOM:

```
cat simple-web-app.cyclonedx.json | head -50
```

Observe the structure:
- `metadata` - SBOM creation info
- `components` - List of all dependencies
- `vulnerabilities` - Known issues (some SBOMs include this)

View the XML SBOM:

```
cat simple-web-app.cyclonedx.xml | head -50
```

Both represent the same data in different formats.

## Part 2: Scan the SBOM

Scan using armis-cli:

```
armis-cli scan sbom simple-web-app.cyclonedx.json --output findings.txt
```

Expected output shows:
- Total components analyzed
- Vulnerabilities found
- Severity breakdown (CRITICAL, HIGH, MEDIUM, LOW, INFO)

## Part 3: Analyze Findings by Component

View full findings:

```
cat findings.txt
```

Count findings by component:

```
grep "Component:" findings.txt | sort | uniq -c
```

Identify most vulnerable component:

```
grep -i "critical\|high" findings.txt | head -10
```

## Part 4: Map Vulnerabilities to CVEs

Look for CVE references in findings:

```
grep -i "CVE" findings.txt
```

Each CVE points to the National Vulnerability Database where you can research:
- Affected versions
- CVSS score
- Remediation advice
- Exploitability

## Part 5: Generate Multiple Output Formats

Generate JSON for programmatic processing:

```
armis-cli scan sbom simple-web-app.cyclonedx.json --output findings.json --format JSON
```

Parse the JSON:

```
cat findings.json | grep '"severity"' | sort | uniq -c
```

Generate SARIF for IDE integration:

```
armis-cli scan sbom simple-web-app.cyclonedx.json --output findings.sarif --format SARIF
```

## Key Concepts

**SBOM** - A complete list of components in software, including versions and dependencies.

**CycloneDX** - Open standard format for SBOM (supports JSON, XML, Protobuf).

**CPE** - Common Platform Enumeration - standardized way to name software components.

**NVD** - National Vulnerability Database - U.S. government database of vulnerabilities.

**CVE** - Common Vulnerabilities and Exposures - unique ID for each known vulnerability.

## Troubleshooting

**"No vulnerabilities found" when scanning?**

SBOM files may not include vulnerability data. Armis scans the component list against NVD during backend processing. Allow 30-60 seconds for results.

**Scan fails immediately?**

Verify the SBOM is valid:

```
python3 -m json.tool simple-web-app.cyclonedx.json > /dev/null && echo "Valid JSON"
```

Verify armis-cli is installed:

```
armis-cli --version
```

**Output doesn't show expected vulnerabilities?**

Compare to Lab 1.1 (repository scanning). Code scanning (SAST) and component scanning (SCA) often detect different issues. SBOMs focus on known component vulnerabilities.

## Lab Complete

You now understand:
- SBOM formats (CycloneDX JSON/XML)
- How to scan SBOMs with armis-cli
- Mapping vulnerabilities to components
- CVE and NVD lookup basics

## Next Lab

Proceed to Lab 2.2: Lockfile Auditing to scan native package manager lockfiles.
