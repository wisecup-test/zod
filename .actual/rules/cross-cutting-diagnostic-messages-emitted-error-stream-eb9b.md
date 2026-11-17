---
version: 2
name: cross-cutting-diagnostic-messages-emitted-error-stream-eb9b
description: "Console API Error and Warning Stream Logging in Operational Scripts: Diagnostic Messages Emitted Error Stream Include"
metadata:
  actual:
    adr_id: eb9b952c-dbc8-4ffe-bb22-3a099cf76bed
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

# Console API Error and Warning Stream Logging in Operational Scripts: Diagnostic Messages Emitted Error Stream Include

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for operational, verification, and repository maintenance scripts executing in standalone execution contexts.

### Rules

- **R-OPR-001** SHOULD: Diagnostic messages emitted to the error stream include human-actionable remediation instructions alongside the identified violation or failure context.

### Verify

```bash
# Discover the repository project manifest, identify configured script verification tasks, and execute the verification suite
# Inspect the script runner configuration and execute the static code analysis suite to verify error stream logging compliance
```

**Accept when:**
- All repository verification and maintenance scripts execute without throwing unhandled exceptions.
- Script failures and rule violations emit formatted diagnostics exclusively to the standard error stream.
- Process exit status accurately reflects the execution outcome indicated by the emitted console stream.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>