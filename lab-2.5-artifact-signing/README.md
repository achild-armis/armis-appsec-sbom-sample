# Lab 2.5 - Artifact Signing & Verification

Learn to sign and verify SBOMs and artifacts using cryptographic signatures for supply chain integrity and attestation.

## Prerequisites

- Lab 2.1-2.4 complete
- armis-cli 1.1.0+
- Understanding of public-key cryptography
- Optional: openssl or equivalent crypto tools
- API credentials configured

## What You'll Learn

- SBOM signing (CycloneDX with signatures)
- Artifact attestation formats (SLSA, in-toto)
- Signature verification workflows
- Chain of custody documentation
- Certificate pinning
- Tamper detection

## Files in This Lab

- `signed-sbom.cyclonedx.json` - Signed SBOM with metadata
- `signature.sig` - Cryptographic signature (RSA-SHA256)
- `README.md` (this file)

## Part 1: Understand Artifact Signing

Signing proves:
- Authenticity - Who created this artifact?
- Integrity - Has it been modified?
- Non-repudiation - The creator can't deny they signed it.

View signed SBOM:

```
cat signed-sbom.cyclonedx.json | head -30
```

Observe:
- Standard CycloneDX structure
- Metadata includes signing info
- Signature embedded or detached

## Part 2: Signature Types

**Detached Signature** (preferred for CI/CD):
- SBOM file: signed-sbom.cyclonedx.json (unchanged)
- Signature file: signature.sig (separate)
- Benefit: Signature doesn't modify artifact

**Embedded Signature:**
- All data in one file
- Benefit: Single file to distribute
- Risk: Signature field is part of signed content

## Part 3: Generate SBOM Signature

Generate an SBOM:

```bash
armis-cli scan repo . --sbom --sbom-format cyclonedx --sbom-output my-sbom.json
```

Sign it (conceptual - requires your private key):

```bash
openssl dgst -sha256 -sign private-key.pem -out my-sbom.json.sig my-sbom.json

armis-cli sbom sign --key private-key.pem --sbom my-sbom.json
```

## Part 4: Verify Signature

Verify with public key:

```bash
openssl dgst -sha256 -verify public-key.pem -signature my-sbom.json.sig my-sbom.json

armis-cli sbom verify --key public-key.pem --sbom my-sbom.json --signature my-sbom.json.sig
```

Expected output:
- `Verified OK` - Signature matches artifact
- `Verification Failure` - Artifact modified or wrong key

## Part 5: Chain of Custody

Document the supply chain:

```json
{
  "artifact": "signed-sbom.cyclonedx.json",
  "signature": "signature.sig",
  "signed_by": "build-system@acme.com",
  "timestamp": "2026-10-01T14:00:00Z",
  "key_id": "0x1A2B3C4D5E6F7G8H",
  "attestation": {
    "type": "in-toto",
    "builder": "GitHub Actions",
    "environment": "prod-pipeline"
  }
}
```

This proves:
1. Who created it (key ID)
2. When (timestamp)
3. What (SBOM hash)
4. How (build command, environment)
5. Why (materials/inputs)

## Part 6: Integration in CI/CD

GitHub Actions example:

```yaml
- name: Generate SBOM
  run: armis-cli scan repo . --sbom --sbom-format cyclonedx --sbom-output sbom.json

- name: Sign SBOM
  run: |
    openssl dgst -sha256 -sign ${{ secrets.BUILD_KEY }} \
      -out sbom.json.sig sbom.json

- name: Verify Signature (self-test)
  run: |
    openssl dgst -sha256 -verify ${{ secrets.BUILD_PUB }} \
      -signature sbom.json.sig sbom.json

- name: Upload Artifacts
  uses: actions/upload-artifact@v3
  with:
    name: sbom-with-signature
    path: |
      sbom.json
      sbom.json.sig
```

## Part 7: Tamper Detection

Test tamper detection:

```bash
# Original state
openssl dgst -sha256 -verify public-key.pem -signature sbom.json.sig sbom.json
# Output: Verified OK

# Modify the SBOM (simulate tampering)
echo " " >> sbom.json

# Verify again
openssl dgst -sha256 -verify public-key.pem -signature sbom.json.sig sbom.json
# Output: Verification Failure - modification detected!
```

## Part 8: SLSA Framework

SLSA (Supply chain Levels for Software Artifacts) has 4 levels:

**SLSA 1** - Basic provenance: SBOM generated, signed by build system

**SLSA 2** - Authenticated provenance: Signed SBOMs, verified build system

**SLSA 3** - Hardened builds: Isolated build environment, code review

**SLSA 4** - Fully hermetic builds: No external inputs, bit-for-bit reproducible

This lab focuses on SLSA 1-2. SLSA 3-4 require infrastructure hardening.

## Key Concepts

**Signature** - Cryptographic proof of authorship and integrity.

**Public Key Infrastructure (PKI)** - System for managing trust via certificates.

**Attestation** - Signed statement about artifact provenance.

**Chain of Custody** - Documented ownership and handling history.

**Tamper Detection** - Verification fails if artifact modified.

**SLSA** - Framework for supply chain security practices.

## Lab Complete

You now understand:
- SBOM signing and verification
- Cryptographic attestation
- Chain of custody documentation
- CI/CD integration
- SLSA framework basics
- Tamper detection

Curriculum complete: Labs 2.1-2.5 mastered.
