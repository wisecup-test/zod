---
version: 2
name: cross-cutting-schema-declarations-colocated-module-bou-06c2
description: "Adopt Zod for Boundary Schema Validation and Parsing: Schema Declarations Colocated Module Boundary Definitions"
metadata:
  actual:
    adr_id: 06c2f3e3-c61f-4f10-bcb6-98eca391fdbc
    status: accepted
    candidate_group_id: fbb66e81-14fa-4010-b455-96af3f3a2042
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adopt Zod for Boundary Schema Validation and Parsing: Schema Declarations Colocated Module Boundary Definitions

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for:
- All public module interfaces and resolution entry points accepting external input data.
- Boundary parsing routines that process untrusted or polymorphic payloads.

### Rules

- **R-LM-001** SHOULD: Schema declarations SHOULD be colocated with module boundary definitions to maintain synchronization between static contracts and runtime rules.

### Verify

- Discover and run the repository verification scripts to verify that all schema parse invocations execute successfully against test inputs.
- Execute the project test suite to verify that boundary validation logic correctly parses valid data and rejects invalid inputs.

**Accept when:**

- All input parsing invocations execute through defined validation schemas without unhandled validation failures on valid inputs.
- The project test suite passes with full verification of boundary inputs against declared schema specifications.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated test suite execution verifying input validation behavior across module boundaries.
- Verified by: Static analysis and peer code review of export definitions and boundary entry points.
- Violation handling: Pull requests with unvalidated boundary inputs or manual type assertions will be blocked until schema validation is introduced.
- Violation handling: Direct commits bypassing validation rules will trigger automated review failure.
- Exception process: Submit an architectural review request documenting technical constraints that preclude schema validation for specific low-level performance paths.
- Exception process: Obtain explicit sign-off from module maintainers before implementing custom parsing routines.
</enforcement>
