---
version: 2
name: cross-cutting-before-implementing-integrating-validati-f724
description: "Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Before Implementing Integrating Validation Modules Consumer"
metadata:
  actual:
    adr_id: f724b42a-e7c3-490a-8737-64f06cd045b8
    status: accepted
    candidate_group_id: b1d967e1-d9ff-4665-b9a4-a3d48eb98cfa
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Before Implementing Integrating Validation Modules Consumer

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for core schema type definitions, parsing logic, validation error generation, issue collection, and localized message formatting modules within the validation library package.

### Rules

- **R-ZOD-001** MUST: Before implementing or integrating with validation modules, locate the repository dependency manifest and inspect the authoritative lock artifact to verify the exact resolved version of the library.

### Verify

```bash
# Discover and run the project's test execution script from the repository manifest
# Locate and run the repository typecheck script
# Identify and execute the static analysis script
```

**Accept when:**
- The project test suite passes completely with all schema validation and error handling scenarios verifying expected issue formats.
- The typecheck command completes with zero diagnostic errors across all schema type definitions and error utilities.
- Static analysis confirms strict compliance with module boundary rules and absence of inline error message formatting in schema types.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>