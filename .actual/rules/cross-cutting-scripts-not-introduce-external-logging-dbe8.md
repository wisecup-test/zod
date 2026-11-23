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

These rules are ALWAYS ACTIVE for:
- Operational, verification, and repository maintenance scripts executing in standalone execution contexts.
- Diagnostic, warning, and failure reporting within automated validation routines.

### Rules

- **R-L-001** MUST_NOT: Scripts MUST NOT introduce external logging frameworks or transport libraries when native runtime console methods satisfy diagnostic reporting requirements.

### Verify

- Discover the repository project manifest, identify configured script verification tasks, and execute the verification suite to ensure all script checks pass.
- Inspect the script runner configuration and execute the static code analysis suite to verify error stream logging compliance.

**Accept when:**

- All repository verification and maintenance scripts execute without throwing unhandled exceptions.
- Script failures and rule violations emit formatted diagnostics exclusively to the standard error stream.
- Process exit status accurately reflects the execution outcome indicated by the emitted console stream.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline executing repository verification and static check scripts.
- Verified by: Peer code review for all new and modified repository scripts.
- Violation handling: Continuous integration checks fail when verification scripts encounter unhandled error conditions.
- Violation handling: Pull requests introducing external logging dependencies or routing script errors to standard output are blocked.
- Exception process: Submit an architectural review request detailing why native runtime console error streams cannot satisfy operational telemetry requirements.
</enforcement>
