---
version: 2
name: cross-cutting-schema-evaluation-components-expose-stan-a1c9
description: "Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Schema Evaluation Components Expose Standardized Execution"
metadata:
  actual:
    adr_id: a1c964f9-557c-41fe-8ca4-c3b85185f2bd
    status: accepted
    candidate_group_id: b1d967e1-d9ff-4665-b9a4-a3d48eb98cfa
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Schema Evaluation Components Expose Standardized Execution

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for core schema type definitions, parsing logic, validation error generation, issue collection, and localized message formatting modules.

### Rules

- **R-ZOD-001** MUST: Schema evaluation components MUST expose standardized execution interfaces through safeParse and parse methods to deliver consistent result containers and issue propagation.

### Verify

```bash
# Discover the test execution script from the repository manifest and run it
# Locate the typecheck script within the project manifest and execute it
# Identify the static analysis script from project configuration and run it
```

**Accept when:**
- The project test suite passes completely with all schema validation and error handling scenarios verifying expected issue formats.
- The typecheck command completes with zero diagnostic errors across all schema type definitions and error utilities.
- Static analysis confirms strict compliance with module boundary rules and absence of inline error message formatting in schema types.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline executing repository test and typecheck scripts, along with peer code review, enforces these constraints.
</enforcement>