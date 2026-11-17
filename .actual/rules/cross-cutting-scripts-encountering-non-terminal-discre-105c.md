---
version: 2
name: cross-cutting-scripts-encountering-non-terminal-discre-105c
description: "Console API Error and Warning Stream Logging in Operational Scripts: Scripts Encountering Non Terminal Discrepancies Route"
metadata:
  actual:
    adr_id: 105c2df0-676d-4049-bd78-2374a16c0f79
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

# Console API Error and Warning Stream Logging in Operational Scripts: Scripts Encountering Non Terminal Discrepancies Route

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for all operational, verification, and repository maintenance scripts executing in standalone execution contexts.

### Rules

- **R-CNS-001** MAY: Scripts encountering non-terminal discrepancies MAY route advisories to the runtime console warning stream instead of terminating execution.
- **R-CNS-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-CNS-003** MANDATORY: Before writing code that uses a versioned library, the developer MUST find the dependency manifest, identify the build tool, inspect the repository lock or resolution artifact for exact versions, look up official documentation for that exact version, confirm API existence, and re-verify per dependency at point of use.
- **R-CNS-004** MANDATORY: Construct error diagnostic strings with explicit failure summaries followed by actionable remediation steps.
- **R-CNS-005** MANDATORY: Ensure script processes return non-zero exit codes whenever terminal failure messages are emitted to the error stream.
- **R-CNS-006** MANDATORY: Sanitize all dynamic values and environment variables before interpolating them into console diagnostic messages.

### Verify

```bash
# Discover the repository project manifest, identify configured script verification tasks, and execute the verification suite:
# (Execute your project's test/verification command here, e.g., npm test or equivalent)

# Inspect the script runner configuration and execute static code analysis:
# (Execute your project's lint/static check command here)
```

**Accept when:**
- All repository verification and maintenance scripts execute without throwing unhandled exceptions.
- Script failures and rule violations emit formatted diagnostics exclusively to the standard error stream.
- Process exit status accurately reflects the execution outcome indicated by the emitted console stream.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>