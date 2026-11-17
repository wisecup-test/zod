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

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** SHOULD: Core translation modules SHOULD isolate check evaluations, registries, and schema processors into independent modular boundaries within the core subsystem.
- **R-CORE-002** MANDATORY: All schema processor additions must implement the standard traversal context interface and propagate the seen-node cache across recursive calls.
- **R-CORE-003** MANDATORY: Newly introduced schema checks and registry entries must maintain bidirectional compatibility with existing processor definitions.
- **R-CORE-004** MANDATORY: Restrict deep cloning strictly to non-primitive default value nodes that require mutation isolation.

### Verify

```bash
# Discover and run the project repository validation suite for core module type-checking and unit test suites.
# Discover and execute the repository integration test suite verifying JSON schema generation across complex and cyclic schema fixtures.
# (Note: Specific tool commands must be discovered from the repository manifest/build configuration per discovery policy)
```

**Accept when:**
- All unit tests for schema processors and generators pass without errors or circular reference exceptions.
- Static type analysis across all core modules completes with zero diagnostic warnings or type mismatch errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. All modifications touching core schema processor or generator modules require peer code review and passing automated CI pipelines.
</enforcement>