---
version: 2
name: cross-cutting-before-implementing-invoking-validation-ed69
description: "Adoption of Zod for Schema Definition and Input Validation: Before Implementing Invoking Validation Schemas Consumer"
metadata:
  actual:
    adr_id: ed694c91-91b2-4003-a06f-d1d0da7d493e
    status: accepted
    candidate_group_id: d82ab627-4321-406c-a644-2305a03bee19
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of Zod for Schema Definition and Input Validation: Before Implementing Invoking Validation Schemas Consumer

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for:
- All runtime input validation and payload parsing across module boundaries.
- Data ingestion points where external or untrusted structures must conform to defined schemas.

### Rules

- **R-LM-001** MUST: Before implementing or invoking validation schemas, the consumer MUST inspect the repository lock artifact to determine the exact resolved dependency version and verify API compatibility against official documentation.

### Verify

- Discover the project's verification and test scripts from the repository manifest and execute them.
- Execute the repository test suite to confirm that schema validation runs without errors across all module formats.

**Accept when:**

- All schema validation parsing logic executes successfully across all supported module targets.
- Repository verification scripts complete with zero exit codes and no schema parsing errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Continuous integration pipelines executing automated test suites.
- Verified by: Peer code review verifying that boundary inputs pass through Zod schema validation.
- Violation handling: Pull requests bypassing schema parsing for boundary inputs will be blocked during review.
- Violation handling: Test failures resulting from unhandled schema validation errors will block deployment.
- Exception process: Exceptions must be submitted via architectural review with documented rationale for bypassing schema validation.
</enforcement>
