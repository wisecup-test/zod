---
version: 2
name: cross-cutting-before-implementing-modifying-modules-th-2688
description: "semver Library Adoption for Semantic Version Validation and Comparison: Before Implementing Modifying Modules That Depend"
metadata:
  actual:
    adr_id: 26887450-3d02-45d1-83eb-ac60f3462c8b
    status: accepted
    candidate_group_id: 88e3c7ec-b2f5-4acc-b756-5dcd64678f07
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# semver Library Adoption for Semantic Version Validation and Comparison: Before Implementing Modifying Modules That Depend

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for automation scripts, release verification routines, and tooling that parse, compare, or validate package versions, and release gating checks that verify version synchronization across multiple published distributions.

### Rules

- **R-SEMVER-001** MUST: Before implementing or modifying modules that depend on the semver library, engineers MUST inspect the repository lock artifact to determine the exact resolved version and verify that invoked functions conform to that version specification.

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