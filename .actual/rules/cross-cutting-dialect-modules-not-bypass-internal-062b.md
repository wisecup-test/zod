---
version: 2
name: cross-cutting-dialect-modules-not-bypass-internal-062b
description: "Internal Core Module Adoption for Schema Traversal and Transformation: Dialect Modules Not Bypass Internal Core"
metadata:
  actual:
    adr_id: 062b44a3-8751-4199-ae59-60d7d36e742f
    status: accepted
    candidate_group_id: 64424c11-2cbc-426e-8f54-ae38ba571b66
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Adoption for Schema Traversal and Transformation: Dialect Modules Not Bypass Internal Core

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DIALECT-001** SHOULD NOT: Dialect modules SHOULD NOT bypass the internal core utility interfaces to implement ad-hoc structural manipulation primitives.

### Verify

```bash
# Discover and run the project test suite from the repository manifest to verify schema transformation consistency across all dialect modules.
# Discover and execute the project static analysis and lint checks to confirm module dependency boundaries and verify that core modules do not depend on dialect submodules.
```

**Accept when:**
- All schema transformation and traversal tests pass across both full and lightweight dialect implementations.
- Module boundary analysis confirms unidirectional dependencies from dialect transformation modules to the internal core module.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via continuous integration test validation, static analysis checks, and pull request architectural code reviews.
</enforcement>