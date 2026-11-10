---
version: 2
name: cross-cutting-direct-invocations-parse-untrusted-input-230e
description: "Zod Runtime Schema Input Validation: Direct Invocations Parse Untrusted Inputs Enclosed"
metadata:
  actual:
    adr_id: 230e866d-1a43-4243-b1e5-38e876193330
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

# Zod Runtime Schema Input Validation: Direct Invocations Parse Untrusted Inputs Enclosed

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: Direct invocations of parse on untrusted inputs MUST be enclosed within error-handling boundaries to capture validation errors.

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