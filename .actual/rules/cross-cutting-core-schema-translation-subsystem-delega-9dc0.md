---
version: 2
name: cross-cutting-core-schema-translation-subsystem-delega-9dc0
description: "Adoption of json-schema-processors Core Module Architecture: Core Schema Translation Subsystem Delegate Json"
metadata:
  actual:
    adr_id: 9dc059a4-81fb-4d18-b10d-81d8128ee1ad
    status: accepted
    candidate_group_id: 4f3aa984-f581-4fab-b688-1e6017994f30
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Adoption of json-schema-processors Core Module Architecture: Core Schema Translation Subsystem Delegate Json

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for:
- Core schema-to-JSON-schema transformation and generation modules within the library.
- Validation check routines and registries interacting with schema translation pipelines.

### Rules

- **R-LM-001** MUST: The core schema translation subsystem MUST delegate all JSON schema generation and transformation logic through the internal json-schema-processors core module architecture.

### Verify

- Discover and run the project repository validation suite for core module type-checking and unit test suites.
- Discover and execute the repository integration test suite verifying JSON schema generation across complex and cyclic schema fixtures.

**Accept when:**

- All unit tests for schema processors and generators pass without errors or circular reference exceptions.
- Static type analysis across all core modules completes with zero diagnostic warnings or type mismatch errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline running test suites and static analysis verification.
- Verified by: Peer code review mandatory for all modifications touching core schema processor or generator modules.
- Violation handling: Pull requests containing inline schema conversion logic or bypassing the traversal cache are blocked from merging.
- Exception process: Exceptions require formal architectural review and approval by the core library maintainers documented in an ADR amendment.
</enforcement>
