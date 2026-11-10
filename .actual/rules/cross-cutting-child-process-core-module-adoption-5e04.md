---
version: 2
name: cross-cutting-child-process-core-module-adoption-5e04
description: "node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Imports Core Process Execution Module Use"
metadata:
  actual:
    adr_id: 5e046bf6-fd01-4a34-9611-c5ce61d97e77
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

# node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Imports Core Process Execution Module Use

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CP-001** MUST: Imports of the core process execution module MUST use the explicit protocol prefix rather than bare module specifiers

### Verify

```bash
# Discover and execute the repository verification scripts declared in the root dependency manifest
# Discover and run static code inspection and typechecking suites across automation scripts to validate module import compliance
```

**Accept when:**
- All repository maintenance and triage scripts import process execution capabilities using the explicit protocol prefix
- Static validation and code inspection verification suites complete with zero errors across all repository scripts

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>