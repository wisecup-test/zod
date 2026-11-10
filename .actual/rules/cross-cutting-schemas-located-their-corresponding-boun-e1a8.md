---
version: 2
name: cross-cutting-schemas-located-their-corresponding-boun-e1a8
description: "Adoption of zod for Runtime Schema Validation and Parsing: Schemas Located Their Corresponding Boundary Interface"
metadata:
  actual:
    adr_id: e1a8a852-1421-4b66-b006-6312fae93ea4
    status: accepted
    candidate_group_id: 3e4f306d-7388-4290-bc8e-3639ded660c1
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of zod for Runtime Schema Validation and Parsing: Schemas Located Their Corresponding Boundary Interface

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** SHOULD: Schemas SHOULD be co-located with their corresponding boundary interface definitions to maintain schema synchronization.
- **R-ZOD-002** MANDATORY: Construct reusable schema objects for shared boundary primitives to prevent redundant declarations.
- **R-ZOD-003** MANDATORY: Infer static types directly from schema definitions to maintain synchronization between compile-time and runtime models.
- **R-ZOD-004** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: (1) Find the dependency manifest in the repo. (2) Identify the build tool. (3) Inspect the repository lock or resolution artifact to determine the exact resolved version. (4) Look up official documentation/changelog/API reference for that exact version without relying solely on training-data recall. (5) Confirm every API, class, or function exists in that exact version's documentation before using it. (6) Re-run steps 3-5 per dependency at point of use for version-sensitive behavior.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute validation suites.
# Discover and run the project test execution command to verify schema parsing tests pass across all module entrypoints.
```

**Accept when:**
- All boundary inputs are validated via schema parsing without manual type casting.
- Verification suites pass with schema validation tests confirming rejection of invalid inputs and acceptance of valid inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests bypassing schema validation on external inputs are blocked from merging. Code review flags any unvalidated boundary type assertions for refactoring.
</enforcement>