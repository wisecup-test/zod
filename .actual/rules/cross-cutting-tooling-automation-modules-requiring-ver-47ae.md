---
version: 2
name: cross-cutting-tooling-automation-modules-requiring-ver-47ae
description: "semver Library Adoption for Semantic Version Validation and Comparison: Tooling Automation Modules Requiring Version Parsing"
metadata:
  actual:
    adr_id: 47aea12e-418b-47f1-9a33-1a703320125f
    status: accepted
    candidate_group_id: 88e3c7ec-b2f5-4acc-b756-5dcd64678f07
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# semver Library Adoption for Semantic Version Validation and Comparison: Tooling Automation Modules Requiring Version Parsing

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for automation scripts, release verification routines, and tooling that parse, compare, or validate package versions.

### Rules

- **R-SEMVER-001** MUST: Tooling and automation modules requiring version parsing, comparison, or compatibility validation MUST use the semver library rather than custom string manipulation or regular expressions.

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
Claude Code MUST NOT skip or defer verification. Verification by automated continuous integration checks and peer code review is mandatory; pull requests containing custom version parsing or unhandled version discrepancies are blocked from merging.
</enforcement>