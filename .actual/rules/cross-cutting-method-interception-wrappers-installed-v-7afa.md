---
version: 2
name: cross-cutting-method-interception-wrappers-installed-v-7afa
description: "Method Interception Middleware for Compiled Execution in Core Schema Engine: Method Interception Wrappers Installed Via Compiled"
metadata:
  actual:
    adr_id: 7afa685e-719d-4101-904b-38a6b464ad53
    status: accepted
    candidate_group_id: ec121c99-6a31-4a67-8d1c-83bb9701913c
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Method Interception Middleware for Compiled Execution in Core Schema Engine: Method Interception Wrappers Installed Via Compiled

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-MIM-001** MUST: Method interception wrappers installed via compiled method installers MUST preserve the original function signature, parameter passing, and return value shapes of both safe parsing and throwing parsing operations.

### Verify

```bash
# Discover and execute the project validation test suite to confirm parity between compiled fast paths and baseline parsing implementations.
# Discover and execute the project static analysis and linting scripts to verify compliance with internal boundary interception conventions.
```

**Accept when:**
- All core parsing and schema validation tests execute and pass when compiled method middleware is engaged.
- Fallback validation behavior executes identically to the uncompiled base implementation whenever the compiled parser returns an invalid sentinel.
- Dynamic property assignments in tree-traversal helpers do not alter or pollute prototype structures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated test suites validating compiled parsing parity against baseline parsing execution and static analysis review must pass. Pull requests that bypass method interception wrappers in favor of direct destructive mutation are blocked.
</enforcement>