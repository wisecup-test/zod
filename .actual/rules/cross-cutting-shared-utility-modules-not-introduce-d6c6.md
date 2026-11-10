---
version: 2
name: cross-cutting-shared-utility-modules-not-introduce-d6c6
description: "ZodError Centralized Validation Error Representation Architecture: Shared Utility Modules Not Introduce Dependencies"
metadata:
  actual:
    adr_id: d6c6e3bd-3c11-4660-83c7-6aae50eb207e
    status: accepted
    candidate_group_id: 2a760602-eb59-42b6-93ff-193614615ecc
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# ZodError Centralized Validation Error Representation Architecture: Shared Utility Modules Not Introduce Dependencies

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for schema parsing, validation execution pipelines, error message localization, and core error representation modules.

### Rules

- **R-ZOD-001** MUST_NOT: Shared utility modules MUST NOT introduce dependencies on concrete schema parsing routines to prevent circular module dependencies.

### Verify

```bash
# Discover the test runner defined in the project configuration manifest and execute the test suite
# Discover the static analysis and type checking script configured in the project repository and run it
# Inspect the project dependency resolution artifact to confirm module import boundaries
```

**Accept when:**
- All schema parsing and localization test suites pass without validation issue schema mismatches.
- Automated static type verification passes with zero type errors across module boundaries consuming ZodError and shared utility functions.
- Validation error emissions consistently conform to the standardized issue descriptors defined by ZodError across all configured locales.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>