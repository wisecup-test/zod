---
version: 2
name: cross-cutting-core-translation-modules-isolate-check-2c64
description: "Adoption of json-schema-processors Core Module Architecture: Core Translation Modules Isolate Check Evaluations"
metadata:
  actual:
    adr_id: 2c645c58-b493-4f5e-a9c0-a7497d37cea5
    status: accepted
    candidate_group_id: 4f3aa984-f581-4fab-b688-1e6017994f30
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Adoption of json-schema-processors Core Module Architecture: Core Translation Modules Isolate Check Evaluations

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for:
- Core schema-to-JSON-schema transformation and generation modules within the library.
- Validation check routines and registries interacting with schema translation pipelines.

### Rules

- **R-LM-001** SHOULD: Core translation modules SHOULD isolate check evaluations, registries, and schema processors into independent modular boundaries within the core subsystem.

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
