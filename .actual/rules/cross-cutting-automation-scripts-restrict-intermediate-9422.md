---
version: 2
name: cross-cutting-automation-scripts-restrict-intermediate-9422
description: "Ephemeral In-Memory Map Collections for Script Execution Data Storage: Automation Scripts Restrict Intermediate Data Caching"
metadata:
  actual:
    adr_id: 942292c9-e207-4469-ae12-530ba72fac73
    status: accepted
    candidate_group_id: a2189cd8-12fc-4690-b1f0-49aa79b4142d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Ephemeral In-Memory Map Collections for Script Execution Data Storage: Automation Scripts Restrict Intermediate Data Caching

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Standalone automation and validation scripts requiring transient in-memory indexing or grouping of execution entities.
- Process-bound CLI routines that collect intermediate state without cross-process persistence requirements.

### Rules

- **R-PD-001** MUST: Automation scripts MUST restrict intermediate data caching and index accumulation to process-local, in-memory key-value data structures.

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
