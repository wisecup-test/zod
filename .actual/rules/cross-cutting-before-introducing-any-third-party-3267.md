---
version: 2
name: cross-cutting-before-introducing-any-third-party-3267
description: "Ephemeral In-Memory Map Collections for Script Execution Data Storage: Before Introducing Any Third Party Datastore"
metadata:
  actual:
    adr_id: 32673930-c4a1-4d86-a70b-fe5f2c447246
    status: accepted
    candidate_group_id: a2189cd8-12fc-4690-b1f0-49aa79b4142d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Ephemeral In-Memory Map Collections for Script Execution Data Storage: Before Introducing Any Third Party Datastore

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for standalone automation and validation scripts requiring transient in-memory indexing or grouping of execution entities, and process-bound CLI routines that collect intermediate state without cross-process persistence requirements.

### Rules

- **R-MEM-001** MUST: Before introducing any third-party datastore or caching dependency, engineers MUST inspect the repository lock artifact to determine the exact resolved dependency versions within the ecosystem manifest.

### Verify

```bash
# Discover and execute the repository typechecking script to verify type safety of key-value map operations.
# Discover and run the repository linter and test suite to ensure scripts adhere to memory management and code quality rules.
```

**Accept when:**
- All automation and validation scripts complete successfully with zero memory leak warnings and clean exit codes.
- Typechecking passes without type errors across key-value data structure accessors and mutators.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory for all changes governed by this rule.
</enforcement>