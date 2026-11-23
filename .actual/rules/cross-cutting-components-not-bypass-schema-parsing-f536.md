---
version: 2
name: cross-cutting-components-not-bypass-schema-parsing-f536
description: "Adoption of Zod for Schema Definition and Input Validation: Components Not Bypass Schema Parsing Use"
metadata:
  actual:
    adr_id: f5368f99-0d67-4b4d-9349-3247a838c66e
    status: accepted
    candidate_group_id: d82ab627-4321-406c-a644-2305a03bee19
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of Zod for Schema Definition and Input Validation: Components Not Bypass Schema Parsing Use

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for:
- All runtime input validation and payload parsing across module boundaries.
- Data ingestion points where external or untrusted structures must conform to defined schemas.

### Rules

- **R-LM-001** MUST_NOT: Components MUST NOT bypass schema parsing or use unvalidated type casting on data ingested across boundaries.

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
