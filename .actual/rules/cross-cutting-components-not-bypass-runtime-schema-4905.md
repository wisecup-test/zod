---
version: 2
name: cross-cutting-components-not-bypass-runtime-schema-4905
description: "Zod Schema-Based Runtime Input Validation: Components Not Bypass Runtime Schema Validation"
metadata:
  actual:
    adr_id: 4905fa12-bdf8-48a2-bc6e-0db03b8da31f
    status: accepted
    candidate_group_id: 38b8990c-6d46-441e-b801-6e145df51cbc
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/ai-sdk/**
      - fixtures/drizzle-zod/**
      - fixtures/internal-types/**
---

# Zod Schema-Based Runtime Input Validation: Components Not Bypass Runtime Schema Validation

Scope: applies to `packages/integration/fixtures/ai-sdk/**`, `packages/integration/fixtures/drizzle-zod/**`, `packages/integration/fixtures/internal-types/**`.

These rules are ALWAYS ACTIVE for:
- All incoming network payloads, database integration schemas, AI model structured inputs, and untrusted boundary boundaries.

### Rules

- **R-SCP-001** MUST_NOT: Components MUST NOT bypass runtime schema validation by casting raw external input structures using unverified type assertions.

### Verify

- Discover the repository test runner from the project manifest and execute the schema validation test suite.
- Locate the repository typecheck and linter configurations from the build manifest to verify schema declarations compile without errors.

**Accept when:**

- All boundary input validation tests pass against declared schemas without unhandled runtime exceptions.
- Static type verification confirms that inferred output types align with declared schema definitions across integration boundaries.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated verification suites executing boundary validation test cases.
- Verified by: Static analysis rules preventing unvalidated input ingestion at integration boundaries.
- Verified by: Peer review verification during code integration.
- Violation handling: Pull requests introducing unvalidated boundary inputs or unsanitized type casts are blocked.
- Violation handling: Runtime validation failures at system boundaries are logged and rejected with structured validation errors.
- Exception process: Submit an architectural exception request detailing why schema validation is infeasible at the given boundary.
- Exception process: Require explicit approval from the application security and architecture review teams before bypassing boundary schema parsing.
</enforcement>
