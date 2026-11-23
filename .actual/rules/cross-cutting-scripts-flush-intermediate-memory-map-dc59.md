---
version: 2
name: cross-cutting-scripts-flush-intermediate-memory-map-dc59
description: "Ephemeral In-Memory Map Collections for Script Execution Data Storage: Scripts Flush Intermediate Memory Map Collections"
metadata:
  actual:
    adr_id: dc5907a9-c384-4cd5-a1fe-ed71dd0402e7
    status: accepted
    candidate_group_id: a2189cd8-12fc-4690-b1f0-49aa79b4142d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Ephemeral In-Memory Map Collections for Script Execution Data Storage: Scripts Flush Intermediate Memory Map Collections

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Standalone automation and validation scripts requiring transient in-memory indexing or grouping of execution entities.
- Process-bound CLI routines that collect intermediate state without cross-process persistence requirements.

### Rules

- **R-PD-001** MAY: Scripts MAY flush intermediate in-memory map collections to standard output or standard error streams when reporting batch processing violations or triage summaries.

### Verify

- Discover and execute the repository typechecking script to verify type safety of key-value map operations.
- Discover and run the repository linter and test suite to ensure scripts adhere to memory management and code quality rules.

**Accept when:**

- All automation and validation scripts complete successfully with zero memory leak warnings and clean exit codes.
- Typechecking passes without type errors across key-value data structure accessors and mutators.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline checks enforcing script execution success and static analysis.
- Verified by: Pull request peer review verifying that script state remains process-bound without introducing external datastores.
- Violation handling: Pull requests introducing unapproved external datastores or unmanaged global caching structures will be rejected.
- Exception process: Exceptions requiring persistent caching across script runs must submit an architecture proposal justifying cross-process storage requirements.
</enforcement>
