---
version: 2
name: cross-cutting-core-utility-functions-not-instantiate-613e
description: "Contextual Schema Issue Error Callback Dispatching in Core Utilities: Core Utility Functions Not Instantiate Couple"
metadata:
  actual:
    adr_id: 613e9273-f53e-4e4e-95e8-7247215b697c
    status: accepted
    candidate_group_id: 1df335b8-ed46-4669-9a07-fb77737e330d
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Contextual Schema Issue Error Callback Dispatching in Core Utilities: Core Utility Functions Not Instantiate Couple

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for core schema utility functions that process validation issues and error records, and validation context definitions and schema instance configurations supporting optional error listeners.

### Rules

- **R-UTIL-001** MUST_NOT: Core utility functions MUST NOT instantiate or couple to concrete external logging libraries or global output streams.

### Verify

```bash
# Discover the project test runner from the repository manifest and execute all unit tests governing core schema utility error paths.
# Discover the static analysis tool from the repository configuration and verify compliance with optional callback invocation rules.
```

**Accept when:**
- All unit and regression test suites for core schema utilities pass with zero failures.
- Static analysis confirms that error callbacks are executed exclusively through guarded optional invocation patterns.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated static analysis checks and peer code review.
</enforcement>