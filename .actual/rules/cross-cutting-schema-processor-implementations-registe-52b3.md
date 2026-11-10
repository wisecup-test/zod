---
version: 2
name: cross-cutting-schema-processor-implementations-registe-52b3
description: "Adoption of json-schema-processors Core Module Architecture: Schema Processor Implementations Register Visited Nodes"
metadata:
  actual:
    adr_id: 52b3bf0b-91ee-41ab-8706-fac14949b4bd
    status: accepted
    candidate_group_id: 4f3aa984-f581-4fab-b688-1e6017994f30
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Adoption of json-schema-processors Core Module Architecture: Schema Processor Implementations Register Visited Nodes

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema-to-JSON-schema transformation and generation modules within the library, as well as validation check routines and registries interacting with schema translation pipelines.

### Rules

- **R-SCH-001** MUST: Schema processor implementations MUST register visited schema nodes in the traversal context cache using ctx.seen to prevent circular reference cycles and duplicate processing.

### Verify

```bash
# Discover and run the project repository validation suite for core module type-checking and unit test suites
# Discover and execute the repository integration test suite verifying JSON schema generation across complex and cyclic schema fixtures
```

**Accept when:**
- All unit tests for schema processors and generators pass without errors or circular reference exceptions.
- Static type analysis across all core modules completes with zero diagnostic warnings or type mismatch errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline running test suites and static analysis verification, and peer code review mandatory for all modifications touching core schema processor or generator modules.
</enforcement>