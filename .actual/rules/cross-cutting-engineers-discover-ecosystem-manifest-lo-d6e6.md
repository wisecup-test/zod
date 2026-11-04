---
version: 2
name: cross-cutting-engineers-discover-ecosystem-manifest-lo-d6e6
description: "Adoption of json-schema-processors Core Module Architecture: Engineers Discover Ecosystem Manifest Lock Artifact"
metadata:
  actual:
    adr_id: d6e63927-c2fc-4021-a12b-f55fe3dac5e8
    status: accepted
    candidate_group_id: 4f3aa984-f581-4fab-b688-1e6017994f30
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Adoption of json-schema-processors Core Module Architecture: Engineers Discover Ecosystem Manifest Lock Artifact

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for core schema-to-JSON-schema transformation, generation modules, validation check routines, and registries interacting with schema translation pipelines.

### Rules

- **R-ADR-001** MUST: Engineers MUST discover the ecosystem manifest and lock artifact in the project repository to verify exact resolved dependency versions before implementing or extending core module features.
- **R-ADR-002** MUST: Execute in order for lock-version grounding: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact version, look up official docs/changelog for that exact version, confirm every API/class/function exists before calling, and re-run steps 3-5 per dependency at point of use for version-sensitive behavior.
- **R-ADR-003** MUST: Ensure all schema processor additions implement the standard traversal context interface and propagate the seen-node cache across recursive calls.
- **R-ADR-004** MUST: Verify that newly introduced schema checks and registry entries maintain bidirectional compatibility with existing processor definitions.

### Verify

```bash
# Discover and run the project repository validation suite for core module type-checking and unit test suites
# Discover and execute the repository integration test suite verifying JSON schema generation across complex and cyclic schema fixtures
```

**Accept when:**
- All unit tests for schema processors and generators pass without errors or circular reference exceptions.
- Static type analysis across all core modules completes with zero diagnostic warnings or type mismatch errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. All modifications touching core schema processor or generator modules require peer code review and must not contain inline schema conversion logic or bypass the traversal cache.
</enforcement>