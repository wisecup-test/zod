---
version: 2
name: cross-cutting-consumers-discover-repository-lock-artif-c397
description: "Zod Runtime Schema Input Validation: Consumers Discover Repository Lock Artifact Verify"
metadata:
  actual:
    adr_id: c397c459-3424-4d58-be3e-d5869b0c839e
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

# Zod Runtime Schema Input Validation: Consumers Discover Repository Lock Artifact Verify

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all external data ingestion boundaries, serialized payload parsers, and schema translation utilities, as well as components processing untrusted, dynamic, or externally supplied data structures.

### Rules

- **R-ZOD-001** MUST: Consumers MUST discover the repository lock artifact and verify the exact resolved library version prior to implementing schema validation.

### Verify

```bash
# Discover and execute the project test runner to verify input validation test suites pass successfully.
# Discover and execute the static analysis script to verify schema definitions and usage across boundary modules.
```

**Accept when:**
- All boundary ingestion routines execute Zod schema validation without bypassing parse or safeParse checks.
- Automated test suites confirm malformed inputs are safely rejected before reaching internal business logic.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>