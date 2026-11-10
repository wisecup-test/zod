---
version: 2
name: cross-cutting-schema-metadata-access-reference-resolut-67b6
description: "In-Memory Schema Registry and Reference Cache via Registries Module: Schema Metadata Access Reference Resolution Route"
metadata:
  actual:
    adr_id: 67b66d88-47fd-488f-ac96-add3488ae188
    status: accepted
    candidate_group_id: 28ad3438-82c5-474c-b774-4a2f09b5817d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/**
---

# In-Memory Schema Registry and Reference Cache via Registries Module: Schema Metadata Access Reference Resolution Route

Scope: applies to `packages/zod/src/**`.

These rules are ALWAYS ACTIVE for internal schema registry modules, metadata storage components, schema transformation pipelines, and discriminated union type dispatch mechanisms.

### Rules

- **R-REG-001** MUST: Schema metadata access and reference resolution MUST route through dedicated in-memory registry instances that provide dual mapping by schema object identity and identifier strings.

### Verify

```bash
# Discover and run the repository test command covering registry and reference caching modules
# Discover and execute workspace type checking and linting scripts to verify data access boundaries
```

**Accept when:**
- All unit and integration test suites validating schema registry lookups, dual-map mutations, and reference cache resolution pass with zero errors
- Static type analysis confirms correct parameter and return types for all map access, mutation, and deletion calls without type coercion warnings

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated CI pipelines and peer code review.
</enforcement>