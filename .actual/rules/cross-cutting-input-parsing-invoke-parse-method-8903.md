---
version: 2
name: cross-cutting-input-parsing-invoke-parse-method-8903
description: "Adoption of zod for Runtime Schema Validation and Parsing: Input Parsing Invoke Parse Method Safeparse"
metadata:
  actual:
    adr_id: 8903d056-51af-4e8d-8bf3-b84b7846fb1b
    status: accepted
    candidate_group_id: 3e4f306d-7388-4290-bc8e-3639ded660c1
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of zod for Runtime Schema Validation and Parsing: Input Parsing Invoke Parse Method Safeparse

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for runtime boundaries, module resolution endpoints, and external input data ingestion.

### Rules

- **R-ZOD-001** MUST: Input parsing MUST invoke the parse method or safeParse method on defined schemas rather than performing ad-hoc manual type assertions.

### Verify

```bash
# Discover and execute the project verification script from the repository manifest
# Discover and run the project test execution command to verify schema parsing tests pass across all module entrypoints
```

**Accept when:**
- All boundary inputs are validated via schema parsing without manual type casting.
- Verification suites pass with schema validation tests confirming rejection of invalid inputs and acceptance of valid inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>