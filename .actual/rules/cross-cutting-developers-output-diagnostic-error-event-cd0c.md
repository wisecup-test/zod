---
version: 2
name: cross-cutting-developers-output-diagnostic-error-event-cd0c
description: "Standard Runtime Console Error Logging: Developers Output Diagnostic Error Events Through"
metadata:
  actual:
    adr_id: cd0cb892-307f-40f2-84d3-986246bb775e
    status: accepted
    candidate_group_id: 0318f53e-f66b-41c4-b5c6-a73f38d34e4f
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
      - loaders/**
---

# Standard Runtime Console Error Logging: Developers Output Diagnostic Error Events Through

Scope: applies to `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for:
- All asynchronous error handlers and boundary catch blocks in client and server runtime scopes lacking dedicated telemetry services.

### Rules

- **R-L-001** MUST: Developers MUST output diagnostic error events through runtime console error methods when no dedicated logging service is configured for the module scope.

### Verify

- Discover and execute the project verification scripts through the repository build system to check for code analysis and linting compliance.
- Run repository test suites to ensure error handling paths and diagnostic outputs function without unhandled promise rejections.

**Accept when:**

- Automated static analysis verification passes without reporting unhandled exception suppressions.
- Error dispatch sites conform to contextual messaging guidelines across all target modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Static analysis and code review checks confirming diagnostic messaging adheres to standard error reporting practices.
- Violation handling: Code review failure and pull request rejection for silent failure suppression or non-compliant error logging.
- Exception process: Submit an architectural change request proposing a centralized logging adoption when structured telemetry is required.
</enforcement>
