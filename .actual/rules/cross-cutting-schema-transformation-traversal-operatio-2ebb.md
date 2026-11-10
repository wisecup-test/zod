---
version: 2
name: cross-cutting-schema-transformation-traversal-operatio-2ebb
description: "Internal Core Module Adoption for Schema Traversal and Transformation: Schema Transformation Traversal Operations Across Dialect"
metadata:
  actual:
    adr_id: 2ebb5883-6419-43d5-82a8-81aa022bb034
    status: accepted
    candidate_group_id: 64424c11-2cbc-426e-8f54-ae38ba571b66
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Adoption for Schema Traversal and Transformation: Schema Transformation Traversal Operations Across Dialect

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all schema transformation and traversal operations across dialect variants.

### Rules

- **R-CORE-001** MUST: Schema transformation and traversal operations across dialect variants MUST import shared visitor algorithms and utility helpers from the internal core module rather than re-implementing schema tree traversal logic locally.

### Verify

```bash
# Discover and run the project test suite from the repository manifest to verify schema transformation consistency across all dialect modules.
# Discover and execute the project static analysis and lint checks to confirm module dependency boundaries and verify that core modules do not depend on dialect submodules.
```

**Accept when:**
- All schema transformation and traversal tests pass across both full and lightweight dialect implementations.
- Module boundary analysis confirms unidirectional dependencies from dialect transformation modules to the internal core module.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>