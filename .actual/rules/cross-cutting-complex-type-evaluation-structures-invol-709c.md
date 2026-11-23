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

These rules are ALWAYS ACTIVE for:
- Core schema type definitions and parsing logic within the validation library package.
- Validation error generation, issue collection, and localized message formatting modules.

### Rules

- **R-LM-001** SHOULD: Complex type evaluation structures involving discriminator matching SHOULD manage lookup resolution through encapsulated mapping constructs to isolate routing logic from error construction.

### Verify

- Discover the project's test execution script from the repository manifest and run the test suite to verify schema validation and error reporting behavior.
- Locate the repository typecheck script within the project manifest and run it to validate type compatibility across schema modules and error interfaces.
- Identify the static analysis script from the project configuration and execute it to ensure no prohibited cross-module references or unapproved error constructions exist.

**Accept when:**

- The project test suite passes completely with all schema validation and error handling scenarios verifying expected issue formats.
- The typecheck command completes with zero diagnostic errors across all schema type definitions and error utilities.
- Static analysis confirms strict compliance with module boundary rules and absence of inline error message formatting in schema types.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline executing repository test and typecheck scripts.
- Verified by: Peer code review verifying that schema types delegate to the centralized error subsystem and omit direct localization bindings.
- Violation handling: Pull requests introducing direct error formatting or bypassing centralized error utilities are rejected at code review.
- Violation handling: Build failures triggered by type mismatches or failing validation error tests block automated merging.
- Exception process: Exceptions for specialized low-overhead parsing utilities must be submitted via an architectural change request and approved by the core library maintainers.
</enforcement>
