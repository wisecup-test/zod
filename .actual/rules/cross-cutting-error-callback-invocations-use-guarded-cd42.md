---
version: 2
name: cross-cutting-error-callback-invocations-use-guarded-cd42
description: "Contextual Schema Issue Error Callback Dispatching in Core Utilities: Error Callback Invocations Use Guarded Optional"
metadata:
  actual:
    adr_id: cd4254f3-e387-4958-88cd-47f296a6cf47
    status: accepted
    candidate_group_id: 1df335b8-ed46-4669-9a07-fb77737e330d
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Contextual Schema Issue Error Callback Dispatching in Core Utilities: Error Callback Invocations Use Guarded Optional

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema utility functions that process validation issues and error records, and validation context definitions and schema instance configurations supporting optional error listeners.

### Rules

- **R-ERR-001** MUST: Error callback invocations MUST use guarded optional execution patterns so that missing telemetry handlers never abort validation processing.

### Verify

```bash
# Discover the project test runner from the repository manifest and execute all unit tests governing core schema utility error paths.
# Discover the static analysis tool from the repository configuration and verify compliance with optional callback invocation rules.
```

**Accept when:**
- All unit and regression test suites for core schema utilities pass with zero failures.
- Static analysis confirms that error callbacks are executed exclusively through guarded optional invocation patterns.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is enforced via automated static analysis checks executed during continuous integration and peer code reviews.
</enforcement>