---
version: 2
name: cross-cutting-dialect-specific-schema-transformation-m-6ef1
description: "Internal Core Module Adoption for Schema Traversal and Transformation: Dialect Specific Schema Transformation Modules Bind"
metadata:
  actual:
    adr_id: 6ef1283e-fc58-41f5-8313-4613bf5f9170
    status: accepted
    candidate_group_id: 64424c11-2cbc-426e-8f54-ae38ba571b66
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Adoption for Schema Traversal and Transformation: Dialect Specific Schema Transformation Modules Bind

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all schema dialect implementation and transformation code within the configured scope.

### Rules

- **R-CORE-001** MUST: Dialect-specific schema transformation modules MUST bind traversal operations to local schema definitions while keeping traversal mechanics centralized in the internal core module.

### Verify

```bash
# Discover and run the project test suite from the repository manifest to verify schema transformation consistency across all dialect modules.
# Discover and execute the project static analysis and lint checks to confirm module dependency boundaries and verify that core modules do not depend on dialect submodules.
```

**Accept when:**
- All schema transformation and traversal tests pass across both full and lightweight dialect implementations.
- Module boundary analysis confirms unidirectional dependencies from dialect transformation modules to the internal core module.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration test validation and static analysis checks must be enforced to prevent duplicate traversal logic or circular imports.
</enforcement>