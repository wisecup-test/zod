---
version: 2
name: cross-cutting-external-data-payloads-dynamic-inputs-dfab
description: "Zod Runtime Schema Input Validation: External Data Payloads Dynamic Inputs Ingestion"
metadata:
  actual:
    adr_id: dfab6fe1-92f7-4701-a6e9-b6b52d35cc51
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

# Zod Runtime Schema Input Validation: External Data Payloads Dynamic Inputs Ingestion

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all external data ingestion boundaries, serialized payload parsers, and schema translation utilities, as well as components processing untrusted, dynamic, or externally supplied data structures.

### Rules

- **R-ZOD-001** MUST: All external data payloads and dynamic inputs at ingestion boundaries MUST be validated using Zod schema definitions before domain processing.

### Verify

```bash
# Discover and execute the project test runner to verify input validation test suites pass successfully.
# Discover and execute the static analysis script to verify schema definitions and usage across boundary modules.
```

**Accept when:**
- All boundary ingestion routines execute Zod schema validation without bypassing parse or safeParse checks.
- Automated test suites confirm malformed inputs are safely rejected before reaching internal business logic.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>