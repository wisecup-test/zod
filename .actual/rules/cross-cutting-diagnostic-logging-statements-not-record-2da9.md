---
version: 2
name: cross-cutting-diagnostic-logging-statements-not-record-2da9
description: "Standard Runtime Console Error Logging: Diagnostic Logging Statements Not Record Unredacted"
metadata:
  actual:
    adr_id: 2da952b3-00fa-43cc-b491-6a1938a99ef8
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

# Standard Runtime Console Error Logging: Diagnostic Logging Statements Not Record Unredacted

Scope: applies to `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all asynchronous error handlers and boundary catch blocks in client and server runtime scopes lacking dedicated telemetry services.

### Rules

- **R-LOG-001** MUST_NOT: Diagnostic logging statements MUST_NOT record unredacted authorization tokens or sensitive environment configurations.

### Verify

```bash
# Discover and execute project verification scripts through the repository build system
# Run repository test suites to ensure error handling paths and diagnostic outputs function without unhandled promise rejections
```

**Accept when:**
- Automated static analysis verification passes without reporting unhandled exception suppressions.
- Error dispatch sites conform to contextual messaging guidelines across all target modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by static analysis and code review checks confirming diagnostic messaging adheres to standard error reporting practices.
</enforcement>