---
version: 2
name: cross-cutting-child-process-core-module-adoption-5aab
description: "node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Long Running High Throughput Subprocesses Consume"
metadata:
  actual:
    adr_id: 5aab3be0-09b3-453e-9173-c8aa67c5c96a
    status: accepted
    candidate_group_id: 420288a8-2a72-4517-858a-135d93066c1f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - .claude/skills/triage/scripts/**
      - scripts/**
---

# node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Long Running High Throughput Subprocesses Consume

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Repository automation scripts, maintenance utilities, and triage workflows executing external commands or system utilities

### Rules

- **R-LM-001** SHOULD: Long-running or high-throughput subprocesses SHOULD consume output asynchronously via streams rather than buffering unbounded output in memory

### Verify

- Discover and execute the repository verification scripts declared in the root dependency manifest
- Discover and run static code inspection and typechecking suites across automation scripts to validate module import compliance

**Accept when:**

- All repository maintenance and triage scripts import process execution capabilities using the explicit protocol prefix
- Static validation and code inspection verification suites complete with zero errors across all repository scripts

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks executing repository verification suites on every proposed change
- Verified by: Peer review validation of module imports and process error handling in all automation scripts
- Violation handling: Proposed changes containing bare module imports or unhandled process executions are rejected until brought into compliance
- Exception process: Exceptions require documented architectural justification and explicit review approval from repository maintainers
</enforcement>
