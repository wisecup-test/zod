---
version: 2
name: cross-cutting-when-registering-unregistering-schema-me-299e
description: "In-Memory Schema Registry and Reference Cache via Registries Module: When Registering Unregistering Schema Metadata Registry"
metadata:
  actual:
    adr_id: 299e6598-a758-4522-bf46-40c1507710c2
    status: accepted
    candidate_group_id: 28ad3438-82c5-474c-b774-4a2f09b5817d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/**
---

# In-Memory Schema Registry and Reference Cache via Registries Module: When Registering Unregistering Schema Metadata Registry

Scope: applies to `packages/zod/src/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-REG-001** MUST: When registering or unregistering schema metadata in the registry, components MUST synchronize mutations across both the schema object map and identifier map using corresponding set and delete operations to prevent orphan entries.

### Verify

```bash
# Discover and run the repository test command covering registry and reference caching modules
# Discover and execute workspace type checking and linting scripts to verify data access boundaries
```

**Accept when:**
- All unit and integration test suites validating schema registry lookups, dual-map mutations, and reference cache resolution pass with zero errors
- Static type analysis confirms correct parameter and return types for all map access, mutation, and deletion calls without type coercion warnings

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>