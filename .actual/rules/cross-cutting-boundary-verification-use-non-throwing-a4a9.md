---
version: 2
name: cross-cutting-boundary-verification-use-non-throwing-a4a9
description: "Zod Schema-Based Runtime Input Validation: Boundary Verification Use Non Throwing Parsing"
metadata:
  actual:
    adr_id: a4a96d4e-112e-4192-8d02-68d52147f239
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

# Zod Schema-Based Runtime Input Validation: Boundary Verification Use Non Throwing Parsing

Scope: applies to `packages/integration/fixtures/ai-sdk/**`, `packages/integration/fixtures/drizzle-zod/**`, `packages/integration/fixtures/internal-types/**`.

These rules are ALWAYS ACTIVE for all incoming network payloads, database integration schemas, AI model structured inputs, and untrusted boundary boundaries.

### Rules

- **R-ZOD-001** MUST: Boundary verification MUST use non-throwing parsing methods such as safeParse to evaluate payload validity and handle failure states deterministically.

### Verify

```bash
# Discover the repository test runner from the project manifest and execute the schema validation test suite.
# Locate the repository typecheck and linter configurations from the build manifest to verify schema declarations compile without errors.
```

**Accept when:**
- All boundary input validation tests pass against declared schemas without unhandled runtime exceptions.
- Static type verification confirms that inferred output types align with declared schema definitions across integration boundaries.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>