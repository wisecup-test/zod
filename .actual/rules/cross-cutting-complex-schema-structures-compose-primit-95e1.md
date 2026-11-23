---
version: 2
name: cross-cutting-complex-schema-structures-compose-primit-95e1
description: "Adoption of Zod for Schema Definition and Safe Parse Validation: Complex Schema Structures Compose Primitive Validators"
metadata:
  actual:
    adr_id: 95e1b0ee-8196-4c60-ba1c-ab3ee31ce4db
    status: accepted
    candidate_group_id: b4f55bd5-a322-4c04-b31c-7702542d2a0c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - play.ts
      - scripts/**
---

# Adoption of Zod for Schema Definition and Safe Parse Validation: Complex Schema Structures Compose Primitive Validators

Scope: applies to `play.ts`, `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Runtime data validation across scripts and operational entry points
- Schema definition and input boundary verification for untrusted data payloads

### Rules

- **R-LM-001** SHOULD: Complex schema structures SHOULD compose primitive schema validators into object schemas rather than implementing custom parsing logic.

### Verify

- Discover the repository test runner from project configuration and execute the schema validation test suite.
- Run the project static analysis and linting scripts to verify compliance with non-throwing validation patterns.

**Accept when:**

- All schema validation tests execute and pass with zero unhandled exceptions.
- Input validation call sites use safeParse and handle validation failure cases explicitly.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks executing repository test suites
- Verified by: Peer code reviews verifying schema definitions and safeParse usage
- Violation handling: Pull requests introducing throwing parse methods or unvalidated inputs are rejected during code review.
- Violation handling: Existing non-compliant validation call sites must be refactored before merging.
- Exception process: Submit an architectural exception request detailing why standard schema validation is inapplicable.
- Exception process: Obtain approval from the technical lead and document the boundary isolation in module documentation.
</enforcement>
