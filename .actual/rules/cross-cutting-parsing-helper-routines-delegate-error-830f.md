---
version: 2
name: cross-cutting-parsing-helper-routines-delegate-error-830f
description: "ZodError Centralized Validation Error Representation Architecture: Parsing Helper Routines Delegate Error Issue"
metadata:
  actual:
    adr_id: 830ff52d-3f73-4985-85e3-fcd647bbd1a5
    status: accepted
    candidate_group_id: 2a760602-eb59-42b6-93ff-193614615ecc
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# ZodError Centralized Validation Error Representation Architecture: Parsing Helper Routines Delegate Error Issue

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for all schema parsing, validation execution pipelines, validation error message localization and formatting modules, and core error representation and issue construction helper modules.

### Rules

- **R-ZOD-001** MUST: Parsing helper routines MUST delegate error issue construction to centralized error utility functions rather than instantiating ad-hoc error shapes.

### Verify

```bash
# Discover and execute the test runner covering parsing utilities and error localization
# Discover and run static analysis / type checking to verify module import resolution and type consistency
# Inspect project dependency resolution artifact to confirm all module imports align with declared dependency boundaries
```

**Accept when:**
- All schema parsing and localization test suites pass without validation issue schema mismatches.
- Automated static type verification passes with zero type errors across module boundaries consuming ZodError and shared utility functions.
- Validation error emissions consistently conform to the standardized issue descriptors defined by ZodError across all configured locales.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and test suite validation must successfully execute to confirm adherence to centralized ZodError issue construction.
</enforcement>