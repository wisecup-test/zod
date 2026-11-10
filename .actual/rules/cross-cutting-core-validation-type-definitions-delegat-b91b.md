---
version: 2
name: cross-cutting-core-validation-type-definitions-delegat-b91b
description: "Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Core Validation Type Definitions Delegate Diagnostic"
metadata:
  actual:
    adr_id: b91bd0c4-1162-4c4f-bb5c-d461bd2133aa
    status: accepted
    candidate_group_id: b1d967e1-d9ff-4665-b9a4-a3d48eb98cfa
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Core Validation Type Definitions Delegate Diagnostic

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for core schema type definitions, parsing logic, validation error generation, issue collection, and localized message formatting modules within the validation library package.

### Rules

- **R-ZOD-001** MUST: Core validation type definitions MUST delegate all validation diagnostic emissions and issue formatting to the centralized ZodError module abstraction rather than constructing bespoke error objects.

### Verify

```bash
# Discover and run the project's test execution script
# Discover and run the repository typecheck script
# Discover and run the static analysis script
```

**Accept when:**
- The project test suite passes completely with all schema validation and error handling scenarios verifying expected issue formats.
- The typecheck command completes with zero diagnostic errors across all schema type definitions and error utilities.
- Static analysis confirms strict compliance with module boundary rules and absence of inline error message formatting in schema types.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>