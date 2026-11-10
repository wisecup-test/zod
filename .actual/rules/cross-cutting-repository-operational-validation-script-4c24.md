---
version: 2
name: cross-cutting-repository-operational-validation-script-4c24
description: "Console API Error and Warning Stream Logging in Operational Scripts: Repository Operational Validation Scripts Emit Failure"
metadata:
  actual:
    adr_id: 4c24ce81-86dd-4677-b50f-a376fc655257
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

# Console API Error and Warning Stream Logging in Operational Scripts: Repository Operational Validation Scripts Emit Failure

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for all operational, verification, and repository maintenance scripts executing in standalone execution contexts.

### Rules

- **R-OPV-001** MUST: Repository operational and validation scripts MUST emit failure notifications, mismatch reports, and diagnostic messages exclusively through the runtime console error stream rather than standard output.

### Verify

```bash
# Discover the repository project manifest, identify configured script verification tasks, and execute the verification suite to ensure all script checks pass.
# Inspect the script runner configuration and execute the static code analysis suite to verify error stream logging compliance.
```

**Accept when:**
- All repository verification and maintenance scripts execute without throwing unhandled exceptions.
- Script failures and rule violations emit formatted diagnostics exclusively to the standard error stream.
- Process exit status accurately reflects the execution outcome indicated by the emitted console stream.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration checks fail when verification scripts encounter unhandled error conditions, and pull requests introducing external logging dependencies or routing script errors to standard output are blocked.
</enforcement>