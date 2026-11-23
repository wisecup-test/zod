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

These rules are ALWAYS ACTIVE for:
- Internal schema registry modules and metadata storage components
- Schema transformation and JSON schema translation pipelines
- Discriminated union type dispatch and cached lookup mechanisms

### Rules

- **R-DAP-001** MUST: When registering or unregistering schema metadata in the registry, components MUST synchronize mutations across both the schema object map and identifier map using corresponding set and delete operations to prevent orphan entries.

### Verify

- # Discover and run the repository test command covering registry and reference caching modules
- # Discover and execute workspace type checking and linting scripts to verify data access boundaries

**Accept when:**

- All unit and integration test suites validating schema registry lookups, dual-map mutations, and reference cache resolution pass with zero errors
- Static type analysis confirms correct parameter and return types for all map access, mutation, and deletion calls without type coercion warnings

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline executing repository test and lint scripts
- Verified by: Peer code review verifying synchronized dual-map mutations and structured traversal cleanup
- Violation handling: Pull requests containing uncoordinated map mutations, unindexed linear searches, or unmanaged reference loops are blocked from merging until corrected
- Exception process: Exceptions require written justification submitted to the architecture review team documenting why an isolated linear search or alternative caching strategy is necessary
</enforcement>
