# Lab 2.3 - Dependency Gating & Policy Enforcement

Learn how to enforce security policies on dependencies using gating rules, exceptions, and CI/CD integration.

## Prerequisites

- Lab 2.1-2.2 complete
- armis-cli 1.1.0+
- JSON policy files
- API credentials configured

## What You'll Learn

- Policy definition and structure
- Gating rules (severity thresholds, license blocking)
- Exception management and approvals
- Whitelist configuration
- CI/CD integration for automated gating
- Policy violations and remediation

## Files in This Lab

- `gating-policy.json` - Base policy with 6 rules
- `complex-app-sbom.cyclonedx.json` - SBOM with policy violations
- `README.md` (this file)

## Part 1: Understand Policy Structure

View the policy:

```
cat gating-policy.json | head -50
```

Observe:
- `rules` - Individual security gates (severity, license, deprecated)
- `exceptions` - Approved violations with expiration dates
- `whitelist` - Trusted packages/vendors
- `report_thresholds` - Acceptable violation counts

## Part 2: Load Complex SBOM

View the complex SBOM:

```
cat complex-app-sbom.cyclonedx.json | grep '"name"' | head -20
```

This SBOM has:
- 15+ components (vs. 8 in Lab 2.1)
- Mix of CRITICAL, HIGH, MEDIUM vulnerabilities
- Deprecated and outdated packages
- License issues (copyleft detection)

## Part 3: Scan with Policy

Scan the SBOM and apply policy:

```
armis-cli scan repo . --sbom complex-app-sbom.cyclonedx.json \
  --fail-on CRITICAL,HIGH \
  --output policy-results.txt
```

Expected output:
- Findings matching severity levels
- Policy violations (CRITICAL fails build)
- Warnings (HIGH limited to 3)
- Deprecated packages flagged

## Part 4: Analyze Policy Violations

Count violations by severity:

```
grep -i "CRITICAL\|HIGH\|MEDIUM" policy-results.txt | sort | uniq -c
```

Identify which packages violate the policy:

```
grep -i "package\|deprecated" policy-results.txt | head -10
```

## Part 5: Apply Exceptions

View exceptions in policy:

```
cat gating-policy.json | grep -A 5 '"exceptions"'
```

Exceptions allow:
- Temporary approval (express-4.16.2 until Q4)
- Lab environment only (lodash in training)
- Time-limited windows (expires: date)

Understanding when to grant vs. deny exceptions is critical:

**GRANT** (temporary):
- In-production components with migration plan
- Training/lab environments (time-limited)
- Known risk with documented remediation

**DENY** (no exception):
- Lab environment beyond training window
- No documented remediation
- Repeated violations in same component

## Part 6: Whitelist Trusted Sources

View whitelist:

```
cat gating-policy.json | grep -A 5 '"whitelist"'
```

Whitelist patterns:
- Internal services (always approved)
- Vendor partner packages
- Curated open-source organizations

Pattern matching uses glob/prefix:
- `github.com/achild-armis/*` matches all Armis org repos
- `@company/` matches all npm scoped packages

## Part 7: CI/CD Integration

In a CI pipeline, gate the build:

```bash
armis-cli scan repo . --sbom complex-app-sbom.cyclonedx.json \
  --fail-on CRITICAL,HIGH \
  --exit-code 1 \
  && echo "✓ Build passes policy" \
  || echo "✗ Build fails: policy violations"
```

In GitHub Actions:

```yaml
- name: Check policy
  run: |
    armis-cli scan repo . --sbom complex-app-sbom.cyclonedx.json \
      --fail-on CRITICAL,HIGH
```

Build stops if thresholds exceeded.

## Key Concepts

**Policy** - Set of security gates applied to components.

**Gating Rule** - Individual policy condition (e.g., fail on CRITICAL).

**Exception** - Time-limited approval to violate a rule.

**Whitelist** - Trusted packages/vendors exempt from rules.

**Exit Code** - 0 (pass), 1 (policy violation).

## Troubleshooting

**"Exit code 1 but no findings?"**

Check report thresholds — they may allow findings without failing:

```
grep -A 5 '"report_thresholds"' gating-policy.json
```

**Policy too strict?**

Adjust thresholds or add whitelist patterns. Regenerate policy and re-scan.

**Exception expired?**

Policy violations trigger again on expiration. Renew or remove the component.

## Lab Complete

You now understand:
- Policy structure and rules
- Exception management
- Whitelisting trusted sources
- CI/CD gating workflows
- Policy-driven remediation

## Next Lab

Proceed to Lab 2.4: Supply Chain Attacks to learn detection patterns.
