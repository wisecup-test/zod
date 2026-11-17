---
version: 2
name: cross-cutting-child-process-core-module-adoption-722b
description: "node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Engineers Discover Ecosystem Lock Artifact Verify"
metadata:
  actual:
    adr_id: 722b381e-ec32-44ce-8dfb-abb2929f11ee
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

# node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Engineers Discover Ecosystem Lock Artifact Verify

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for all repository automation scripts, maintenance utilities, and triage workflows executing external commands or system utilities.

### Rules

- **R-CP-001** MUST: Engineers MUST discover the ecosystem lock artifact and verify runtime dependency constraints before introducing or modifying dependencies in automation scripts.

### Verify

```bash
# Discover and execute the repository verification scripts declared in the root dependency manifest
# Discover and run static code inspection and typechecking suites across automation scripts to validate module import compliance
```

**Accept when:**
- All repository maintenance and triage scripts import process execution capabilities using the explicit protocol prefix
- Static validation and code inspection verification suites complete with zero errors across all repository scripts

<enforcement>
Claude Code MUST NOT skip or defer verification. All proposed changes containing bare module imports or unhandled process executions are rejected until brought into compliance.
</enforcement>