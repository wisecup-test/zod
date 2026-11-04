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
- **R-CORE-002** MANDATORY: Ensure all schema processor additions implement the standard traversal context interface and propagate the seen-node cache across recursive calls.
- **R-CORE-003** MANDATORY: Verify that newly introduced schema checks and registry entries maintain bidirectional compatibility with existing processor definitions.
- **R-CORE-004** MANDATORY (DISCOVERY POLICY): Omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.
- **R-CORE-005** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact resolved version, look up official docs/changelog for that exact version, confirm every API/class/function exists in that version, and re-run per dependency at point of use for version-sensitive behavior.

### Verify

```bash
# Discover and run the project repository validation suite for core module type-checking and unit test suites.
# Discover and execute the repository integration test suite verifying JSON schema generation across complex and cyclic schema fixtures.
```

**Accept when:**
- All unit tests for schema processors and generators pass without errors or circular reference exceptions.
- Static type analysis across all core modules completes with zero diagnostic warnings or type mismatch errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration pipeline running test suites and static analysis verification, accompanied by mandatory peer code review for all modifications touching core schema processor or generator modules. Pull requests containing inline schema conversion logic or bypassing the traversal cache are blocked from merging.
</enforcement>