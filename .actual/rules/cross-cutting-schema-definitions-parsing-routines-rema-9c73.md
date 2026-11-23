---
version: 2
name: cross-cutting-schema-definitions-parsing-routines-rema-9c73
description: "Adoption of Zod for Schema Definition and Input Validation: Schema Definitions Parsing Routines Remain Structurally"
metadata:
  actual:
    adr_id: 9c73417f-a378-47de-9494-8d4c99e5fa6e
    status: accepted
    candidate_group_id: d82ab627-4321-406c-a644-2305a03bee19
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of Zod for Schema Definition and Input Validation: Schema Definitions Parsing Routines Remain Structurally

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for:
- All runtime input validation and payload parsing across module boundaries.
- Data ingestion points where external or untrusted structures must conform to defined schemas.

### Rules

- **R-LM-001** SHOULD: Schema definitions and parsing routines SHOULD remain structurally identical across all module compilation targets supported by the repository.

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
