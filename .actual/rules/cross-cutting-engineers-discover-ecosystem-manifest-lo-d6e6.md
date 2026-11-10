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

These rules are ALWAYS ACTIVE for core schema-to-JSON-schema transformation and generation modules within the library, and validation check routines and registries interacting with schema translation pipelines.

### Rules

- **R-ARCH-001** MUST: Engineers MUST discover the ecosystem manifest and lock artifact in the project repository to verify exact resolved dependency versions before implementing or extending core module features.
- **R-ARCH-002** MUST: Ensure all schema processor additions implement the standard traversal context interface and propagate the seen-node cache across recursive calls.
- **R-ARCH-003** MUST: Verify that newly introduced schema checks and registry entries maintain bidirectional compatibility with existing processor definitions.

### Verify

```bash
# Discover and run the project repository validation suite for core module type-checking and unit test suites
# Discover and execute the repository integration test suite verifying JSON schema generation across complex and cyclic schema fixtures
```

**Accept when:**
- All unit tests for schema processors and generators pass without errors or circular reference exceptions.
- Static type analysis across all core modules completes with zero diagnostic warnings or type mismatch errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests containing inline schema conversion logic or bypassing the traversal cache are blocked from merging.
</enforcement>