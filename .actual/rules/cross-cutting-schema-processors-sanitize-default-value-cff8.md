---
version: 2
name: cross-cutting-schema-processors-sanitize-default-value-cff8
description: "Adoption of json-schema-processors Core Module Architecture: Schema Processors Sanitize Default Values Through"
metadata:
  actual:
    adr_id: cff8c40f-d0a0-4d93-aa07-981dbf68ef75
    status: accepted
    candidate_group_id: 4f3aa984-f581-4fab-b688-1e6017994f30
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Adoption of json-schema-processors Core Module Architecture: Schema Processors Sanitize Default Values Through

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema-to-JSON-schema transformation and generation modules within the library, as well as validation check routines and registries interacting with schema translation pipelines.

### Rules

- **R-SCP-001** SHOULD: Schema processors SHOULD sanitize default values through structural deep-cloning serialization prior to emitting JSON schema definitions.
- **R-SCP-002** MANDATORY: Ensure all schema processor additions implement the standard traversal context interface and propagate the seen-node cache across recursive calls.
- **R-SCP-003** MANDATORY: Verify that newly introduced schema checks and registry entries maintain bidirectional compatibility with existing processor definitions.

### Verify

```bash
# Discover and run the project repository validation suite for core module type-checking and unit test suites
# Discover and execute the repository integration test suite verifying JSON schema generation across complex and cyclic schema fixtures
```

**Accept when:**
- All unit tests for schema processors and generators pass without errors or circular reference exceptions.
- Static type analysis across all core modules completes with zero diagnostic warnings or type mismatch errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline runs test suites and static analysis verification. Pull requests containing inline schema conversion logic or bypassing the traversal cache are blocked from merging.
</enforcement>