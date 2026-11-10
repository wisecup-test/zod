---
version: 2
name: cross-cutting-interception-wrappers-not-override-targe-7301
description: "Method Interception Middleware for Compiled Execution in Core Schema Engine: Interception Wrappers Not Override Target Parsing"
metadata:
  actual:
    adr_id: 7301b029-e138-4aa8-a3d5-da052daadb87
    status: accepted
    candidate_group_id: ec121c99-6a31-4a67-8d1c-83bb9701913c
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Method Interception Middleware for Compiled Execution in Core Schema Engine: Interception Wrappers Not Override Target Parsing

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-INT-001** MUST_NOT: Interception wrappers MUST NOT override target parsing methods destructively without retaining an executable reference to the original source implementation.

### Verify

```bash
# Discover and execute project validation test suite to confirm parity between compiled fast paths and baseline parsing implementations.
# Discover and execute project static analysis and linting scripts to verify compliance with internal boundary interception conventions.
```

**Accept when:**
- All core parsing and schema validation tests execute and pass when compiled method middleware is engaged.
- Fallback validation behavior executes identically to the uncompiled base implementation whenever the compiled parser returns an invalid sentinel.
- Dynamic property assignments in tree-traversal helpers do not alter or pollute prototype structures.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>