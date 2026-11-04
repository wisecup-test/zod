---
version: 2
name: cross-cutting-components-not-execute-linear-filter-89fc
description: "In-Memory Schema Registry and Reference Cache via Registries Module: Components Not Execute Linear Filter Find"
metadata:
  actual:
    adr_id: 89fc3859-fc8c-4bdb-84f2-8c6cf20c925b
    status: accepted
    candidate_group_id: 28ad3438-82c5-474c-b774-4a2f09b5817d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/**
---

# In-Memory Schema Registry and Reference Cache via Registries Module: Components Not Execute Linear Filter Find

Scope: applies to `packages/zod/src/**`.

These rules are ALWAYS ACTIVE for internal schema registry modules, metadata storage components, schema transformation pipelines, JSON schema translation pipelines, and discriminated union type dispatch mechanisms.

### Rules

- **R-REG-001** MUST_NOT: Components MUST_NOT execute linear filter or find operations across raw check or definition arrays when an indexed map can provide constant-time key lookups.

### Verify

```bash
# Discover and run the repository test command covering registry and reference caching modules
# Discover and execute workspace type checking and linting scripts to verify data access boundaries
```

**Accept when:**
- All unit and integration test suites validating schema registry lookups, dual-map mutations, and reference cache resolution pass with zero errors
- Static type analysis confirms correct parameter and return types for all map access, mutation, and deletion calls without type coercion warnings

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>