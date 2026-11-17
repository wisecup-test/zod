---
version: 2
name: cross-cutting-schema-validation-issue-logging-dispatch-cff6
description: "Contextual Schema Issue Error Callback Dispatching in Core Utilities: Schema Validation Issue Logging Dispatched Through"
metadata:
  actual:
    adr_id: cff66f49-99a7-4951-9772-1917d398035f
    status: accepted
    candidate_group_id: 1df335b8-ed46-4669-9a07-fb77737e330d
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Contextual Schema Issue Error Callback Dispatching in Core Utilities: Schema Validation Issue Logging Dispatched Through

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema utility functions that process validation issues and error records, and validation context definitions and schema instance configurations supporting optional error listeners.

### Rules

- **R-SCH-001** MUST: Schema validation issue logging MUST be dispatched through optional contextual error callbacks defined on the schema definition instance or execution context rather than via direct logging framework invocations.

### Verify

```bash
# Discover the project test runner from the repository manifest and execute all unit tests governing core schema utility error paths.
# Discover the static analysis tool from the repository configuration and verify compliance with optional callback invocation rules.
```

**Accept when:**
- All unit and regression test suites for core schema utilities pass with zero failures.
- Static analysis confirms that error callbacks are executed exclusively through guarded optional invocation patterns.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>