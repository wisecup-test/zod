---
version: 2
name: cross-cutting-transient-traversal-state-containers-man-6fab
description: "Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Transient Traversal State Containers Managing Cyclic"
metadata:
  actual:
    adr_id: 6fab5a3e-f789-4712-933a-47b68c78e7e4
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

# Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Transient Traversal State Containers Managing Cyclic

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all schema processing, compilation, serialization, and traversal code interacting with schema metadata registries.

### Rules

- **R-SCH-001** MUST: Transient traversal state containers managing cyclic reference resolution and recursion tracking MUST invoke explicit deletion operations upon exiting recursion scopes to prevent reference retention.

### Verify

```bash
# Discover the workspace test execution script in the project manifest and run the suite covering schema registries and compiler traversal.
# Discover the repository static analysis script and verify zero direct property mutations on schema instances across data access modules.
```

**Accept when:**
- All registry unit and integration test suites pass with complete assertion coverage on bidirectional lookup, registration, and deletion.
- Memory profiling tests confirm traversal context maps release all tracking references upon traversal completion without leakage.
- Static type checks verify that schema definitions remain read-only and all external metadata access occurs through registry abstractions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>