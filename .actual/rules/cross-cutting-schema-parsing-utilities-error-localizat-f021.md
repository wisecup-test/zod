---
version: 2
name: cross-cutting-schema-parsing-utilities-error-localizat-f021
description: "ZodError Centralized Validation Error Representation Architecture: Schema Parsing Utilities Error Localization Modules"
metadata:
  actual:
    adr_id: f0216996-ef5f-4156-b29d-f254d01c740e
    status: accepted
    candidate_group_id: 2a760602-eb59-42b6-93ff-193614615ecc
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# ZodError Centralized Validation Error Representation Architecture: Schema Parsing Utilities Error Localization Modules

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for schema parsing, validation execution pipelines, validation error message localization, formatting modules, and core error representation modules.

### Rules

- **R-ZOD-001** MUST: All schema parsing utilities and error localization modules MUST import and use ZodError as the unified representation for validation issue types and error data structures.

### Verify

```bash
# Discover the test runner defined in the project configuration manifest and execute the test suite covering parsing utilities and error localization.
# Discover the static analysis and type checking script configured in the project repository and run it to verify module import resolution and type consistency across core error modules.
# Inspect the project dependency resolution artifact to confirm all module imports align with declared dependency boundaries.
```

**Accept when:**
- All schema parsing and localization test suites pass without validation issue schema mismatches.
- Automated static type verification passes with zero type errors across module boundaries consuming ZodError and shared utility functions.
- Validation error emissions consistently conform to the standardized issue descriptors defined by ZodError across all configured locales.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>