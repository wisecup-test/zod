---
version: 2
name: cross-cutting-when-incorporating-any-versioned-third-734d
description: "Contextual Schema Issue Error Callback Dispatching in Core Utilities: When Incorporating Any Versioned Third Party"
metadata:
  actual:
    adr_id: 734d5f18-cc59-4343-a820-6e3d69cee824
    status: accepted
    candidate_group_id: 1df335b8-ed46-4669-9a07-fb77737e330d
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Contextual Schema Issue Error Callback Dispatching in Core Utilities: When Incorporating Any Versioned Third Party

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema utility functions that process validation issues, error records, and validation context definitions supporting optional error listeners.

### Rules

- **R-OBS-001** MUST: When incorporating any versioned third-party dependency into the observability pipeline, consumers MUST verify the project lock artifact to resolve the exact dependency version prior to use.

### Verify

```bash
# Discover the project test runner from the repository manifest and execute all unit tests governing core schema utility error paths.
# Discover the static analysis tool from the repository configuration and verify compliance with optional callback invocation rules.
```

**Accept when:**
- All unit and regression test suites for core schema utilities pass with zero failures.
- Static analysis confirms that error callbacks are executed exclusively through guarded optional invocation patterns.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis checks executed during continuous integration and peer code review.
</enforcement>