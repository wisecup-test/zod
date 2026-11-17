---
version: 2
name: cross-cutting-automated-verification-routines-not-impl-f9e2
description: "semver Library Adoption for Semantic Version Validation and Comparison: Automated Verification Routines Not Implement Custom"
metadata:
  actual:
    adr_id: f9e2bb1d-6d51-4f39-9b07-6e06c89548af
    status: accepted
    candidate_group_id: 88e3c7ec-b2f5-4acc-b756-5dcd64678f07
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# semver Library Adoption for Semantic Version Validation and Comparison: Automated Verification Routines Not Implement Custom

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-SEMVER-001** MUST_NOT: Automated verification routines MUST NOT implement custom version precedence comparison or ad-hoc range evaluation algorithms.

### Verify

```bash
# Discover and execute the project verification script defined in the repository manifest responsible for semver checking.
# Discover and execute the automated lockstep verification script defined in the repository manifest.
```

**Accept when:**
- Version validation routines successfully parse and compare version identifiers using the semver library.
- Lockstep verification halts with an error exit code when version mismatches are detected between synchronized packages.
- All automated verification directives pass without unhandled exceptions or syntax errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>