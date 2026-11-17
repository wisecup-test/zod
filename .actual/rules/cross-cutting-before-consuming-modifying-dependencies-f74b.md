---
version: 2
name: cross-cutting-before-consuming-modifying-dependencies-f74b
description: "Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Before Consuming Modifying Dependencies Within Schema"
metadata:
  actual:
    adr_id: f74bccf2-0ce1-4fb0-ba43-10c549f5ea6a
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

# Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Before Consuming Modifying Dependencies Within Schema

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for schema processing pipelines, serialization/deserialization routines, and compiler constant registration.

### Rules

- **R-META-001** MUST: Before consuming or modifying dependencies within schema processing pipelines, inspect the project resolution artifact to identify the exact locked version of all relevant modules.
- **R-META-002** MUST: Isolate schema-to-metadata associations and bidirectional identifier indices into dedicated registry structures with explicit lifecycle boundaries rather than mutating schema definitions directly.
- **R-META-003** MUST: Maintain transient state collections across schema transformation and compilation operations using contextual traversal structures, cleaning up tracking references upon scope exit.

### Verify

```bash
# Discover workspace test execution script in project manifest and run the suite covering schema registries and compiler traversal
# Discover repository static analysis script and verify zero direct property mutations on schema instances across data access modules
```

**Accept when:**
- All registry unit and integration test suites pass with complete assertion coverage on bidirectional lookup, registration, and deletion.
- Memory profiling tests confirm traversal context maps release all tracking references upon traversal completion without leakage.
- Static type checks verify that schema definitions remain read-only and all external metadata access occurs through registry abstractions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>