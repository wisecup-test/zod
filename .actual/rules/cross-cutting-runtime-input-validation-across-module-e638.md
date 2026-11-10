---
version: 2
name: cross-cutting-runtime-input-validation-across-module-e638
description: "Adoption of zod for Runtime Schema Validation and Parsing: Runtime Input Validation Across Module Boundaries"
metadata:
  actual:
    adr_id: e638b372-30a5-47ff-86f0-2d83f7fa34b6
    status: accepted
    candidate_group_id: 3e4f306d-7388-4290-bc8e-3639ded660c1
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of zod for Runtime Schema Validation and Parsing: Runtime Input Validation Across Module Boundaries

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: All runtime input validation across module boundaries MUST use zod schemas to parse and validate incoming payloads.
- **R-ZOD-002** MANDATORY: Execute the lock-version grounding sequence (manifest discovery, build tool identification, exact lockfile version inspection, API reference verification) before writing code that uses a versioned library.
- **R-ZOD-003** MANDATORY: Infer static types directly from schema definitions to maintain synchronization between compile-time and runtime models, and construct reusable schema objects for shared boundary primitives to prevent redundant declarations.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute validation suites.
# Discover and run the project test execution command to verify schema parsing tests pass across all module entrypoints.
```

**Accept when:**
- All boundary inputs are validated via schema parsing without manual type casting.
- Verification suites pass with schema validation tests confirming rejection of invalid inputs and acceptance of valid inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests bypassing schema validation on external inputs are blocked from merging.
</enforcement>