---
version: 2
name: cross-cutting-engineers-declare-runtime-data-validatio-fd02
description: "Adoption of Zod for Schema Definition and Safe Parse Validation: Engineers Declare Runtime Data Validation Schemas"
metadata:
  actual:
    adr_id: fd023a23-1c41-49c1-8500-11241d0341f4
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

# Adoption of Zod for Schema Definition and Safe Parse Validation: Engineers Declare Runtime Data Validation Schemas

Scope: applies to `play.ts`, `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Runtime data validation across scripts and operational entry points
- Schema definition and input boundary verification for untrusted data payloads

### Rules

- **R-LM-001** MUST: Engineers MUST declare runtime data validation schemas using Zod structural primitives and validate input boundaries using safeParse instead of throwing validation methods.

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
