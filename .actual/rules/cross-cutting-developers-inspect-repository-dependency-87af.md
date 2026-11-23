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

These rules are ALWAYS ACTIVE for:
- Internal schema registry modules and metadata storage components
- Schema transformation and JSON schema translation pipelines
- Discriminated union type dispatch and cached lookup mechanisms

### Rules

- **R-DAP-001** MUST: Developers MUST inspect the repository dependency lock artifact to determine the exact resolved dependency versions before integrating registry and data access components.

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
