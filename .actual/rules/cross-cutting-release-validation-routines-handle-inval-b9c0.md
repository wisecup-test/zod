---
version: 2
name: cross-cutting-release-validation-routines-handle-inval-b9c0
description: "semver Library Adoption for Semantic Version Validation and Comparison: Release Validation Routines Handle Invalid Semantic"
metadata:
  actual:
    adr_id: b9c07034-9af4-4ff7-a931-87494628ff02
    status: accepted
    candidate_group_id: 88e3c7ec-b2f5-4acc-b756-5dcd64678f07
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# semver Library Adoption for Semantic Version Validation and Comparison: Release Validation Routines Handle Invalid Semantic

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Automation scripts, release verification routines, and tooling that parse, compare, or validate package versions.
- Release gating checks that verify version synchronization across multiple published distributions.

### Rules

- **R-LM-001** SHOULD: Release validation routines SHOULD handle invalid semantic version formats gracefully by logging explicit diagnostic errors before halting execution.

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
