---
version: 2
name: cross-cutting-discriminator-variant-dispatch-handlers-3bb0
description: "In-Memory Schema Registry and Reference Cache via Registries Module: Discriminator Variant Dispatch Handlers Initialize Dedicated"
metadata:
  actual:
    adr_id: 3bb07678-5291-42ac-ac24-b04c73eb2975
    status: accepted
    candidate_group_id: 28ad3438-82c5-474c-b774-4a2f09b5817d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/**
---

# In-Memory Schema Registry and Reference Cache via Registries Module: Discriminator Variant Dispatch Handlers Initialize Dedicated

Scope: applies to `packages/zod/src/**`.

These rules are ALWAYS ACTIVE for internal schema registry modules, metadata storage components, schema transformation pipelines, JSON schema translation pipelines, and discriminated union type dispatch and cached lookup mechanisms.

### Rules

- **R-REG-001** SHOULD: Discriminator variant dispatch handlers MUST initialize dedicated option maps to resolve discriminator values to target types rather than evaluating dynamic conditionals at runtime.

### Verify

```bash
# Discover and run the repository test command covering registry and reference caching modules
# Discover and execute workspace type checking and linting scripts to verify data access boundaries
```

**Accept when:**
- All unit and integration test suites validating schema registry lookups, dual-map mutations, and reference cache resolution pass with zero errors
- Static type analysis confirms correct parameter and return types for all map access, mutation, and deletion calls without type coercion warnings

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration and peer code review.
</enforcement>