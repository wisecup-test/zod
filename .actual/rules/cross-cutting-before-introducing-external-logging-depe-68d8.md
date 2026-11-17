---
version: 2
name: cross-cutting-before-introducing-external-logging-depe-68d8
description: "Standard Runtime Console Error Logging: Before Introducing External Logging Dependencies Developers"
metadata:
  actual:
    adr_id: 68d80769-07e2-4b13-8b5b-132e19c4bd40
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

# Standard Runtime Console Error Logging: Before Introducing External Logging Dependencies Developers

Scope: applies to `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all asynchronous error handlers and boundary catch blocks in client and server runtime scopes lacking dedicated telemetry services.

### Rules

- **R-LOG-001** MUST: Before introducing external logging dependencies, developers MUST discover project dependency manifests and verify locked dependency versions according to the mandatory lock-version grounding policy.

### Verify

```bash
# Discover and execute project verification scripts through the repository build system
# Run repository test suites to ensure error handling paths and diagnostic outputs function without unhandled promise rejections
```

**Accept when:**
- Automated static analysis verification passes without reporting unhandled exception suppressions.
- Error dispatch sites conform to contextual messaging guidelines across all target modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification by static analysis and code review checks confirming diagnostic messaging adheres to standard error reporting practices is mandatory.
</enforcement>