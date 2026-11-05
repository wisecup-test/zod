---
version: 2
name: cross-cutting-registry-consumers-expose-helper-retriev-4da3
description: "In-Memory Schema Registry and Reference Cache via Registries Module: Registry Consumers Expose Helper Retrieval Methods"
metadata:
  actual:
    adr_id: 4da3c0d6-b4c8-411a-9cc1-e3e8dc66bf1d
    status: accepted
    candidate_group_id: 28ad3438-82c5-474c-b774-4a2f09b5817d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/**
---

# In-Memory Schema Registry and Reference Cache via Registries Module: Registry Consumers Expose Helper Retrieval Methods

Scope: applies to `packages/zod/src/**`.

These rules are ALWAYS ACTIVE for internal schema registry modules, metadata storage components, schema transformation pipelines, and discriminated union type dispatch mechanisms.

### Rules

- **R-REG-001** MAY: Registry consumers MAY expose helper retrieval methods to query metadata by polymorphic identifier keys.
- **R-REG-002** MANDATORY: Wrap recursive resolution logic in structured try-finally blocks or finalizers ensuring transient processing token deletion executes upon traversal completion to prevent memory leaks and infinite loops.
- **R-REG-003** MANDATORY: Encapsulate deletion operations inside atomic registry methods that purge both identity and identifier maps simultaneously to prevent inconsistent registry state.
- **R-REG-004** MANDATORY: Before writing code that uses a versioned library, execute the lock-version grounding process (find dependency manifest, identify build tool, inspect lock/resolution artifact for exact version, check official docs for that version, confirm APIs exist, re-run per dependency at point of use).

### Verify

```bash
# Discover and run the repository test command covering registry and reference caching modules
# Discover and execute workspace type checking and linting scripts to verify data access boundaries
```

**Accept when:**
- All unit and integration test suites validating schema registry lookups, dual-map mutations, and reference cache resolution pass with zero errors
- Static type analysis confirms correct parameter and return types for all map access, mutation, and deletion calls without type coercion warnings

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests containing uncoordinated map mutations, unindexed linear searches, or unmanaged reference loops are blocked until corrected.
</enforcement>