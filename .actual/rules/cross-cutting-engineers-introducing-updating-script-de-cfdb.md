---
version: 2
name: cross-cutting-engineers-introducing-updating-script-de-cfdb
description: "Console API Error and Warning Stream Logging in Operational Scripts: Engineers Introducing Updating Script Dependencies Inspect"
metadata:
  actual:
    adr_id: cfdbef7d-ff26-4ede-914e-7eed0a51e2f9
    status: accepted
    candidate_group_id: 109ad59f-7122-451e-aab9-f1b755fbbae5
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - .claude/skills/triage/scripts/**
      - scripts/**
---

# Console API Error and Warning Stream Logging in Operational Scripts: Engineers Introducing Updating Script Dependencies Inspect

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for all operational, verification, and repository maintenance scripts executing in standalone execution contexts.

### Rules

- **R-LOG-001** MUST: Engineers introducing or updating script dependencies MUST inspect the project lock artifact to verify the exact resolved version against the dependency manifest before using dependency APIs.

### Verify

```bash
# Discover the repository project manifest, identify configured script verification tasks, and execute the verification suite
# Inspect the script runner configuration and execute the static code analysis suite
```

**Accept when:**
- All repository verification and maintenance scripts execute without throwing unhandled exceptions.
- Script failures and rule violations emit formatted diagnostics exclusively to the standard error stream.
- Process exit status accurately reflects the execution outcome indicated by the emitted console stream.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>