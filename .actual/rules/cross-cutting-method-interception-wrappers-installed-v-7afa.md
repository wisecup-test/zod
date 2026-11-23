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

These rules are ALWAYS ACTIVE for:
- Core schema parsing compilation and method installation routines.
- Internal structural tree traversal and dynamic property initialization utilities.

### Rules

- **R-ISP-001** MUST: Method interception wrappers installed via compiled method installers MUST preserve the original function signature, parameter passing, and return value shapes of both safe parsing and throwing parsing operations.

### Verify

- Discover and execute the project validation test suite to confirm parity between compiled fast paths and baseline parsing implementations.
- Discover and execute the project static analysis and linting scripts to verify compliance with internal boundary interception conventions.

**Accept when:**

- All core parsing and schema validation tests execute and pass when compiled method middleware is engaged.
- Fallback validation behavior executes identically to the uncompiled base implementation whenever the compiled parser returns an invalid sentinel.
- Dynamic property assignments in tree-traversal helpers do not alter or pollute prototype structures.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated test suites validating compiled parsing parity against baseline parsing execution.
- Verified by: Static analysis and architectural review verifying that schema method wrapping adheres to established delegation middleware patterns.
- Violation handling: Pull requests that bypass method interception wrappers in favor of direct destructive mutation are blocked.
- Violation handling: Build pipeline failures on regression test suites that detect divergence between compiled output and baseline parser output.
- Exception process: Propose an architectural amendment demonstrating that the schema execution path cannot be modeled through functional method interception.
- Exception process: Obtain approval from the core engine maintainers before introducing alternative execution hooks.
</enforcement>
