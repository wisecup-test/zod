---
version: 2
name: cross-cutting-core-schema-compilation-transformation-e-1b53
description: "standard-schema Module Adoption: Core Schema Compilation Transformation Error Dispatch"
metadata:
  actual:
    adr_id: 1b534680-3264-41f6-9c71-10498d8078b1
    status: accepted
    candidate_group_id: cde02561-665e-40aa-bc54-b52077956cb9
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# standard-schema Module Adoption: Core Schema Compilation Transformation Error Dispatch

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-SS-001** MUST: Core schema compilation, transformation, and error dispatch modules MUST interface through the standard-schema module contract rather than proprietary internal representations.

### Verify

```bash
# Discover the repository build and test script in the project manifest and execute tests
# Discover the repository linter and type-checker commands from project configuration
# Run the linter, type-checker, and core test suite to verify contract compliance
```

**Accept when:**
- All core schema transformations and error definitions pass automated type-checking and unit test suites verifying conformity to the standard-schema module contracts.
- Dependency analysis confirms no cyclic dependencies or direct bypasses of the standard-schema module in core schema transformation modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>