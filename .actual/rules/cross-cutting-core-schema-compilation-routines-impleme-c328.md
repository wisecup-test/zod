---
version: 2
name: cross-cutting-core-schema-compilation-routines-impleme-c328
description: "Method Interception Middleware for Compiled Execution in Core Schema Engine: Core Schema Compilation Routines Implement Method"
metadata:
  actual:
    adr_id: c328efd5-5117-4440-84b7-40407ebbcc55
    status: accepted
    candidate_group_id: ec121c99-6a31-4a67-8d1c-83bb9701913c
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Method Interception Middleware for Compiled Execution in Core Schema Engine: Core Schema Compilation Routines Implement Method

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** MUST: Core schema compilation routines MUST implement method interception middleware that wraps user-facing parsing methods to execute compiled fast paths with fallback delegation to original method references upon receiving an invalid output sentinel.

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
Claude Code MUST NOT skip or defer verification.
</enforcement>