---
version: 2
name: cross-cutting-modules-evaluating-package-release-parit-d5d8
description: "semver Library Adoption for Semantic Version Validation and Comparison: Modules Evaluating Package Release Parity Across"
metadata:
  actual:
    adr_id: d5d829cb-aa90-4fb2-9f20-88155a7923bb
    status: accepted
    candidate_group_id: 88e3c7ec-b2f5-4acc-b756-5dcd64678f07
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# semver Library Adoption for Semantic Version Validation and Comparison: Modules Evaluating Package Release Parity Across

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Automation scripts, release verification routines, and tooling that parse, compare, or validate package versions.
- Release gating checks that verify version synchronization across multiple published distributions.

### Rules

- **R-LM-001** MUST: Modules evaluating package release parity across registries MUST validate version equality and lockstep alignment via semver comparison utilities.

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
