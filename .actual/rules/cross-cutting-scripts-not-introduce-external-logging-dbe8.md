---
version: 2
name: cross-cutting-scripts-not-introduce-external-logging-dbe8
description: "Console API Error and Warning Stream Logging in Operational Scripts: Scripts Not Introduce External Logging Frameworks"
metadata:
  actual:
    adr_id: dbe881bd-7ecb-46b7-8fa5-165bf7d6b302
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

# Console API Error and Warning Stream Logging in Operational Scripts: Scripts Not Introduce External Logging Frameworks

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for operational, verification, and repository maintenance scripts executing in standalone execution contexts.

### Rules

- **R-LOG-001** MUST_NOT: Scripts MUST NOT introduce external logging frameworks or transport libraries when native runtime console methods satisfy diagnostic reporting requirements.

### Verify

```bash
# Discover the repository project manifest, identify configured script verification tasks, and execute verification/static analysis suites
package_manager=$(find . -maxdepth 2 -name "package.json" -o -name "Cargo.toml" -o -name "go.mod" -o -name "pyproject.toml")
echo "Discovered manifest: $package_manager"
# Execute verification checks according to repository conventions
```

**Accept when:**
- All repository verification and maintenance scripts execute without throwing unhandled exceptions.
- Script failures and rule violations emit formatted diagnostics exclusively to the standard error stream.
- Process exit status accurately reflects the execution outcome indicated by the emitted console stream.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration and peer code review enforce logging compliance; pull requests introducing external logging dependencies are blocked.
</enforcement>