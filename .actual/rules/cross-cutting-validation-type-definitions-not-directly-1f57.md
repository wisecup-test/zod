---
version: 2
name: cross-cutting-validation-type-definitions-not-directly-1f57
description: "Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Validation Type Definitions Not Directly Embed"
metadata:
  actual:
    adr_id: 1f57733e-51c1-4ee5-852d-4395c661967d
    status: accepted
    candidate_group_id: b1d967e1-d9ff-4665-b9a4-a3d48eb98cfa
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Validation Type Definitions Not Directly Embed

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for core schema type definitions, parsing logic, validation error generation, issue collection, and localized message formatting modules within the validation library package.

### Rules

- **R-VAL-001** MUST_NOT: Validation type definitions MUST NOT directly embed locale-specific error string mappings or message formatting routines within type declaration modules.

### Verify

```bash
# Discover and run the project's test execution script from the repository manifest
# Locate and run the repository typecheck script within the project manifest
# Identify and execute the static analysis script from the project configuration
```

**Accept when:**
- The project test suite passes completely with all schema validation and error handling scenarios verifying expected issue formats.
- The typecheck command completes with zero diagnostic errors across all schema type definitions and error utilities.
- Static analysis confirms strict compliance with module boundary rules and absence of inline error message formatting in schema types.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated CI, peer code review, and build checks.
</enforcement>