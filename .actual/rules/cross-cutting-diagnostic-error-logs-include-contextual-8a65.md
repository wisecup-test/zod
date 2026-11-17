---
version: 2
name: cross-cutting-diagnostic-error-logs-include-contextual-8a65
description: "Standard Runtime Console Error Logging: Diagnostic Error Logs Include Contextual Descriptive"
metadata:
  actual:
    adr_id: 8a653c43-d363-41b0-84ba-eac2cfcc3419
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

# Standard Runtime Console Error Logging: Diagnostic Error Logs Include Contextual Descriptive

Scope: applies to `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all asynchronous error handlers and boundary catch blocks in client and server runtime scopes lacking dedicated telemetry services.

### Rules

- **R-LOG-001** MUST: Diagnostic error logs MUST include contextual descriptive strings alongside original caught error objects.

### Verify

```bash
# Discover and execute the project verification scripts through the repository build system to check for code analysis and linting compliance.
# Run repository test suites to ensure error handling paths and diagnostic outputs function without unhandled promise rejections.
```

**Accept when:**
- Automated static analysis verification passes without reporting unhandled exception suppressions.
- Error dispatch sites conform to contextual messaging guidelines across all target modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>