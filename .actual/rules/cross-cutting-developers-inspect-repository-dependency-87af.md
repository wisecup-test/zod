---
version: 2
name: cross-cutting-developers-inspect-repository-dependency-87af
description: "In-Memory Schema Registry and Reference Cache via Registries Module: Developers Inspect Repository Dependency Lock Artifact"
metadata:
  actual:
    adr_id: 87afd918-1b0c-47a9-8de0-8e98563edcda
    status: accepted
    candidate_group_id: 28ad3438-82c5-474c-b774-4a2f09b5817d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/**
---

# In-Memory Schema Registry and Reference Cache via Registries Module: Developers Inspect Repository Dependency Lock Artifact

Scope: applies to `packages/zod/src/**`.

These rules are ALWAYS ACTIVE for internal schema registry modules, metadata storage components, schema transformation pipelines, JSON schema translation pipelines, and discriminated union type dispatch mechanisms.

### Rules

- **R-REG-001** MUST: Developers MUST inspect the repository dependency lock artifact to determine the exact resolved dependency versions before integrating registry and data access components.

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