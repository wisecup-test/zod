---
version: 2
name: cross-cutting-validation-schemas-declare-fine-grained-275e
description: "Zod Schema-Based Runtime Input Validation: Validation Schemas Declare Fine Grained Constraints"
metadata:
  actual:
    adr_id: 275e8210-8fcf-4203-9c00-91ee54ce804a
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

# Zod Schema-Based Runtime Input Validation: Validation Schemas Declare Fine Grained Constraints

Scope: applies to `packages/integration/fixtures/ai-sdk/**`, `packages/integration/fixtures/drizzle-zod/**`, `packages/integration/fixtures/internal-types/**`.

These rules are ALWAYS ACTIVE for:
- All incoming network payloads, database integration schemas, AI model structured inputs, and untrusted boundary boundaries.

### Rules

- **R-SCP-001** SHOULD: Validation schemas SHOULD declare fine-grained constraints on primitive fields, including format, range, and enumeration checks, to enforce domain invariants at the perimeter.

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
