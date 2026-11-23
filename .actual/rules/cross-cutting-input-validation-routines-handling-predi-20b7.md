---
version: 2
name: cross-cutting-input-validation-routines-handling-predi-20b7
description: "Zod Runtime Schema Input Validation: Input Validation Routines Handling Predictable Failure"
metadata:
  actual:
    adr_id: 20b78da0-1348-4151-9a3f-e96c4ecdf43b
    status: accepted
    candidate_group_id: 0b9e35e4-1818-4c41-93b8-39ce7b8dced7
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
      - src/v4/**
---

# Zod Runtime Schema Input Validation: Input Validation Routines Handling Predictable Failure

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for:
- All external data ingestion boundaries, serialized payload parsers, and schema translation utilities.
- Components processing untrusted, dynamic, or externally supplied data structures.

### Rules

- **R-SCP-001** MUST: Input validation routines handling predictable failure control flows MUST use safeParse to inspect validation results without throwing unhandled exceptions.

### Verify

- Discover and execute the project test runner to verify input validation test suites pass successfully.
- Discover and execute the static analysis script to verify schema definitions and usage across boundary modules.

**Accept when:**

- All boundary ingestion routines execute Zod schema validation without bypassing parse or safeParse checks.
- Automated test suites confirm malformed inputs are safely rejected before reaching internal business logic.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks executing repository test suites and contract validation tests.
- Verified by: Peer code reviews ensuring all newly introduced boundary endpoints parse inputs via Zod schemas.
- Violation handling: Pull requests containing unvalidated boundary inputs are blocked from merging until schema checks are added.
- Violation handling: Runtime unhandled input validation exceptions trigger immediate alerting and remediation tickets.
- Exception process: Architecture review board approval documented in an architectural exception record with explicit residual risk acceptance.
- Exception process: Demonstrated benchmark proof showing validation overhead exceeds allowable latency thresholds in critical paths.
</enforcement>
