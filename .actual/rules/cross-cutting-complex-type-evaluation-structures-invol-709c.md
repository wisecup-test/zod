---
version: 2
name: cross-cutting-complex-type-evaluation-structures-invol-709c
description: "Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Complex Type Evaluation Structures Involving Discriminator"
metadata:
  actual:
    adr_id: 709c9ede-46b3-4e32-a898-05dea4a68247
    status: accepted
    candidate_group_id: b1d967e1-d9ff-4665-b9a4-a3d48eb98cfa
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Complex Type Evaluation Structures Involving Discriminator

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for core schema type definitions, parsing logic, validation error generation, issue collection, and localized message formatting modules.

### Rules

- **R-ZOD-001** SHOULD: Complex type evaluation structures involving discriminator matching SHOULD manage lookup resolution through encapsulated mapping constructs to isolate routing logic from error construction.
- **R-ZOD-002** MANDATORY: Ensure all schema type evaluation logic routes through centralized error utilities rather than constructing direct error instances or formatting localized strings.
- **R-ZOD-003** MANDATORY: Maintain distinct boundaries between parsing logic, discriminator resolution maps, and error emission to safeguard modularity and performance.
- **R-ZOD-004** MANDATORY: Adhere to the lock-version grounding process (inspect manifest, identify build tool, inspect lock artifact for exact version, check official documentation for that exact version, confirm APIs before use) before writing code that uses a versioned library.

### Verify

```bash
# Discover the project's test execution script from the repository manifest and run tests
# Locate the repository typecheck script within the project manifest and run it
# Identify the static analysis script from the project configuration and execute it
```

**Accept when:**
- The project test suite passes completely with all schema validation and error handling scenarios verifying expected issue formats.
- The typecheck command completes with zero diagnostic errors across all schema type definitions and error utilities.
- Static analysis confirms strict compliance with module boundary rules and absence of inline error message formatting in schema types.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration and peer code review.
</enforcement>