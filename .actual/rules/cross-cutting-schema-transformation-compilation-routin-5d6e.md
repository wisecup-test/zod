---
version: 2
name: cross-cutting-schema-transformation-compilation-routin-5d6e
description: "Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Schema Transformation Compilation Routines Not Attach"
metadata:
  actual:
    adr_id: 5d6e8a33-c66e-431f-b5ff-9f8e6d1dc341
    status: accepted
    candidate_group_id: d8b3ef21-85e1-4a50-9fc9-84f24d157d45
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
      - src/v4/**
---

# Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Schema Transformation Compilation Routines Not Attach

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all schema processing pipelines, transformation compilation routines, and metadata registry modules.

### Rules

- **R-SCH-001** MUST_NOT: Schema transformation and compilation routines MUST NOT attach transient traversal state, intermediate constants, or resolved references directly to schema instances as mutable properties.

### Verify

```bash
# Discover and run the workspace test execution script covering schema registries and compiler traversal
# Discover and run the repository static analysis script to verify zero direct property mutations on schema instances
```

**Accept when:**
- All registry unit and integration test suites pass with complete assertion coverage on bidirectional lookup, registration, and deletion.
- Memory profiling tests confirm traversal context maps release all tracking references upon traversal completion without leakage.
- Static type checks verify that schema definitions remain read-only and all external metadata access occurs through registry abstractions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated unit and integration tests, peer code reviews, and static analysis checks must be enforced.
</enforcement>