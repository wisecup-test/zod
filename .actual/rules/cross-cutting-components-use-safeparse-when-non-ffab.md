---
version: 2
name: cross-cutting-components-use-safeparse-when-non-ffab
description: "Adoption of zod for Runtime Schema Validation and Parsing: Components Use Safeparse When Non Throwing"
metadata:
  actual:
    adr_id: ffab2c28-f333-4767-83d9-01658057bf3c
    status: accepted
    candidate_group_id: 3e4f306d-7388-4290-bc8e-3639ded660c1
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of zod for Runtime Schema Validation and Parsing: Components Use Safeparse When Non Throwing

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for runtime input parsing and validation within module resolution entrypoints and data contracts interfacing with external inputs across module formats.

### Rules

- **R-ZOD-001** MAY: Components MAY use safeParse when non-throwing error handling is preferred over parse exceptions.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute validation suites.
# Discover and run the project test execution command to verify schema parsing tests pass across all module entrypoints.
```

**Accept when:**
- All boundary inputs are validated via schema parsing without manual type casting.
- Verification suites pass with schema validation tests confirming rejection of invalid inputs and acceptance of valid inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>