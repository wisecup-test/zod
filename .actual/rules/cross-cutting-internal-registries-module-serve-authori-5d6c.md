---
version: 2
name: cross-cutting-internal-registries-module-serve-authori-5d6c
description: "Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Internal Registries Module Serve Authoritative Data"
metadata:
  actual:
    adr_id: 5d6c8f0c-3092-41db-b9f2-ea9b8c96387c
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

# Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Internal Registries Module Serve Authoritative Data

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for schema processing pipelines, compilation, serialization, and deserialization routines requiring external metadata association and bidirectional identity storage.

### Rules

- **R-REG-001** MUST: The internal registries module MUST serve as the authoritative data access abstraction for associating schema definitions with external metadata and bidirectional identifier mappings.
- **R-REG-002** MUST: Instantiate traversal contexts at the root of translation or compilation workflows and pass context instances explicitly down recursive visitor calls.
- **R-REG-003** MUST: Implement bidirectional registry collections with unified registration methods that set both object-keyed and string-keyed associations concurrently.
- **R-REG-004** MUST: Encapsulate deletion operations inside atomic registry methods that purge both primary and secondary indices within a single method call.
- **R-REG-005** MUST: Wrap recursive traversal calls in structured exception-handling blocks that guarantee cleanup of tracking references upon completion.

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