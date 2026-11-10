---
version: 2
name: cross-cutting-memory-cache-stores-isolate-keys-ff35
description: "Ephemeral In-Memory Map Collections for Script Execution Data Storage: Memory Cache Stores Isolate Keys Prefixed"
metadata:
  actual:
    adr_id: ff358350-26c5-4034-b60b-d31ffb2ef028
    status: accepted
    candidate_group_id: a2189cd8-12fc-4690-b1f0-49aa79b4142d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Ephemeral In-Memory Map Collections for Script Execution Data Storage: Memory Cache Stores Isolate Keys Prefixed

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for standalone automation and validation scripts requiring transient in-memory indexing or grouping of execution entities, and process-bound CLI routines collecting intermediate state.

### Rules

- **R-MEM-001** SHOULD: In-memory cache stores SHOULD isolate keys by prefixed domain identifiers when aggregating multiple heterogeneous entity streams within a single execution scope.

### Verify

```bash
# Discover and execute the repository typechecking script to verify type safety of key-value map operations.
# Discover and run the repository linter and test suite to ensure scripts adhere to memory management and code quality rules.
```

**Accept when:**
- All automation and validation scripts complete successfully with zero memory leak warnings and clean exit codes.
- Typechecking passes without type errors across key-value data structure accessors and mutators.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline checks and pull request peer review.
</enforcement>