---
version: 2
name: cross-cutting-schema-translation-compilation-contexts-3c21
description: "In-Memory Schema Registry and Reference Cache via Registries Module: Schema Translation Compilation Contexts Maintain Active"
metadata:
  actual:
    adr_id: 3c21f539-b033-4f7d-8f5c-2ce341cf80d2
    status: accepted
    candidate_group_id: 28ad3438-82c5-474c-b774-4a2f09b5817d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/**
---

# In-Memory Schema Registry and Reference Cache via Registries Module: Schema Translation Compilation Contexts Maintain Active

Scope: applies to `packages/zod/src/**`.

These rules are ALWAYS ACTIVE for schema processing, transformation workflows, internal schema registry modules, metadata storage components, schema transformation and JSON schema translation pipelines, and discriminated union type dispatch and cached lookup mechanisms.

### Rules

- **R-REG-001** MUST: Schema translation and compilation contexts MUST maintain an active processing map that records reference paths during traversal and MUST explicitly delete resolved paths when traversal unwinds to guarantee cycle prevention.
- **R-REG-002** MANDATORY: Execute the lock-version grounding process before writing code that uses a versioned library: find dependency manifest, identify build tool, inspect repository lock/resolution artifact for exact version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps per dependency at point of use.
- **R-REG-003** MANDATORY: Ensure all reference caching layers utilize structured key serialization to avoid ambiguous reference path collisions across disparate namespaces.
- **R-REG-004** MANDATORY: Implement defensive cleanup in traversal contexts using finalizer/try-finally blocks to guarantee deletion of transient processing tokens.
- **R-REG-005** MANDATORY: Encapsulate deletion operations inside atomic registry methods that purge both primary and identifier indices simultaneously to prevent inconsistent registry state.

### Verify

```bash
# Discover and run the repository test command covering registry and reference caching modules
# Discover and execute workspace type checking and linting scripts to verify data access boundaries
```

**Accept when:**
- All unit and integration test suites validating schema registry lookups, dual-map mutations, and reference cache resolution pass with zero errors.
- Static type analysis confirms correct parameter and return types for all map access, mutation, and deletion calls without type coercion warnings.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests containing uncoordinated map mutations, unindexed linear searches, or unmanaged reference loops are blocked from merging until corrected.
</enforcement>