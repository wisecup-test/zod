---
version: 2
name: cross-cutting-common-schema-registries-metadata-resolu-c389
description: "Core Module Architecture for Shared Schema Primitives: Common Schema Registries Metadata Resolution Lookup"
metadata:
  actual:
    adr_id: c3891226-afe0-4d41-8668-d231d2b25b3c
    status: accepted
    candidate_group_id: bec2016e-3f8a-44fb-95a3-11cf67256d04
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Core Module Architecture for Shared Schema Primitives: Common Schema Registries Metadata Resolution Lookup

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CM-001** SHOULD: Access common schema registries and metadata resolution lookup patterns through the standard interfaces exposed by the core module.
- **R-CM-002** MANDATORY: Ensure core module exports expose minimal, highly cohesive utilities and registries required by consumers.
- **R-CM-003** MANDATORY: Maintain unidirectional module references so that the core module never depends on consumer distributions.
- **R-CM-004** MANDATORY: Apply strict internal export boundaries to avoid exposing internal core abstractions as public library API contracts.

### Verify

```bash
# Discover and execute the project boundary analysis check to confirm that all shared imports originate from the core module.
# Discover and run the repository test and validation suite to verify that all distribution flavors successfully integrate with the core module.
```

**Accept when:**
- Dependency boundary analysis passes with zero cross-flavor couplings and all shared traversal logic referencing the core module.
- Repository test suites execute successfully with all modules resolving core registry and utility contracts.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated boundary and module resolution checks, and architecture review during pull requests.
</enforcement>