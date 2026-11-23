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

These rules are ALWAYS ACTIVE for:
- Automation scripts, release verification routines, and tooling that parse, compare, or validate package versions.
- Release gating checks that verify version synchronization across multiple published distributions.

### Rules

- **R-LM-001** MUST: Tooling and automation modules requiring version parsing, comparison, or compatibility validation MUST use the semver library rather than custom string manipulation or regular expressions.

### Verify

- Discover and execute the project verification script defined in the repository manifest responsible for semver checking.
- Discover and execute the automated lockstep verification script defined in the repository manifest.

**Accept when:**

- Version validation routines successfully parse and compare version identifiers using the semver library.
- Lockstep verification halts with an error exit code when version mismatches are detected between synchronized packages.
- All automated verification directives pass without unhandled exceptions or syntax errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks executing repository verification scripts.
- Verified by: Peer code review verifying that version comparison routines utilize the adopted library rather than custom logic.
- Violation handling: Pull requests containing custom version parsing or unhandled version discrepancies are blocked from merging.
- Exception process: Exceptions must be documented with an architectural justification and approved by the engineering leads.
</enforcement>
