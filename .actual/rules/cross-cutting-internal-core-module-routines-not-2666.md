---
version: 2
name: cross-cutting-internal-core-module-routines-not-2666
description: "Internal Core Module Adoption for Schema Traversal and Transformation: Internal Core Module Routines Not Introduce"
metadata:
  actual:
    adr_id: 2666b736-736f-46ce-aeea-55bcf23c66c7
    status: accepted
    candidate_group_id: 64424c11-2cbc-426e-8f54-ae38ba571b66
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Adoption for Schema Traversal and Transformation: Internal Core Module Routines Not Introduce

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ICM-001** MUST_NOT: Internal core module routines MUST NOT introduce circular dependencies by importing dialect-specific schema definitions or dialect transformation modules.

### Verify

```bash
# Discover and run the project test suite from the repository manifest to verify schema transformation consistency across all dialect modules.
# Discover and execute the project static analysis and lint checks to confirm module dependency boundaries and verify that core modules do not depend on dialect submodules.
```

**Accept when:**
- All schema transformation and traversal tests pass across both full and lightweight dialect implementations.
- Module boundary analysis confirms unidirectional dependencies from dialect transformation modules to the internal core module.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration test validation and static analysis checks must verify schema transformation correctness and detect disallowed circular dependencies between internal core modules and dialect modules.
</enforcement>