---
version: 2
name: cross-cutting-child-process-core-module-adoption-707f
description: "node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Repository Automation Maintenance Scripts Use Node"
metadata:
  actual:
    adr_id: 707f586f-1183-4479-acae-289d1551581f
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

# node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Repository Automation Maintenance Scripts Use Node

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for all repository automation scripts, maintenance utilities, and triage workflows executing external commands or system utilities.

### Rules

- **R-CP-001** MUST: Repository automation and maintenance scripts MUST use the node:child_process core module for all external process spawning and command-line execution tasks

### Verify

```bash
# Discover and execute repository verification scripts and static code inspection suites from the root dependency manifest
```

**Accept when:**
- All repository maintenance and triage scripts import process execution capabilities using the explicit protocol prefix
- Static validation and code inspection verification suites complete with zero errors across all repository scripts

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks and peer review validation.
</enforcement>