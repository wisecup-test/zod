---
version: 2
name: cross-cutting-untrusted-data-entering-system-integrati-0b34
description: "Zod Schema-Based Runtime Input Validation: Untrusted Data Entering System Integration Persistence"
metadata:
  actual:
    adr_id: 0b34aae9-0189-4389-829b-cd9886ebb7c5
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

# Zod Schema-Based Runtime Input Validation: Untrusted Data Entering System Integration Persistence

Scope: applies to `packages/integration/fixtures/ai-sdk/**`, `packages/integration/fixtures/drizzle-zod/**`, `packages/integration/fixtures/internal-types/**`.

These rules are ALWAYS ACTIVE for all incoming network payloads, database integration schemas, AI model structured inputs, and untrusted boundary boundaries.

### Rules

- **R-ZOD-001** MUST: All untrusted data entering the system at integration, persistence, and external boundaries MUST be validated against declared zod schemas prior to consumption.

### Verify

```bash
# Discover the repository test runner from the project manifest and execute the schema validation test suite.
# Locate the repository typecheck and linter configurations from the build manifest to verify schema declarations compile without errors.
```

**Accept when:**
- All boundary input validation tests pass against declared schemas without unhandled runtime exceptions.
- Static type verification confirms that inferred output types align with declared schema definitions across integration boundaries.

<enforcement>
Claude Code MUST NOT skip or defer verification. All boundary input data ingestion MUST comply with runtime zod schema validation rules.
</enforcement>