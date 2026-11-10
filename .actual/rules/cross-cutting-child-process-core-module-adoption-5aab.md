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

These rules are ALWAYS ACTIVE for repository automation scripts, maintenance utilities, and triage workflows executing external commands or system utilities.

### Rules

- **R-CHIL-001** SHOULD: Long-running or high-throughput subprocesses SHOULD consume output asynchronously via streams rather than buffering unbounded output in memory.

### Verify

```bash
# Discover and execute repository verification scripts declared in the root dependency manifest
# Run static code inspection and typechecking suites across automation scripts to validate module import compliance
```

**Accept when:**
- All repository maintenance and triage scripts import process execution capabilities using the explicit protocol prefix
- Static validation and code inspection verification suites complete with zero errors across all repository scripts

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory for all proposed changes containing process executions and module imports.
</enforcement>