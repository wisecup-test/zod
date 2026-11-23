---
version: 2
name: cross-cutting-boundary-handlers-not-bypass-schema-4311
description: "Zod Runtime Schema Input Validation: Boundary Handlers Not Bypass Schema Validation"
metadata:
  actual:
    adr_id: 43118ae8-9e03-4a95-a50e-321c048d4d5b
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

# Zod Runtime Schema Input Validation: Boundary Handlers Not Bypass Schema Validation

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for:
- All external data ingestion boundaries, serialized payload parsers, and schema translation utilities.
- Components processing untrusted, dynamic, or externally supplied data structures.

### Rules

- **R-SCP-001** MUST_NOT: Boundary handlers MUST NOT bypass schema validation when deserializing or transforming external payloads.

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
