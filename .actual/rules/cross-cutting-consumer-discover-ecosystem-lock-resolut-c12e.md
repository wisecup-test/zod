---
version: 2
name: cross-cutting-consumer-discover-ecosystem-lock-resolut-c12e
description: "Adoption of zod/mini for Modular Schema Definition and Input Validation: Consumer Discover Ecosystem Lock Resolution Artifact"
metadata:
  actual:
    adr_id: c12e339c-2889-420c-88d3-5c9a3b7ff5bc
    status: accepted
    candidate_group_id: 6019c7a4-9a84-4a99-a2a2-7b9ec4210fe7
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
      - packages/resolution/src/**
      - packages/treeshake/**
---

# Adoption of zod/mini for Modular Schema Definition and Input Validation: Consumer Discover Ecosystem Lock Resolution Artifact

Scope: applies to `packages/bench/**`, `packages/resolution/src/**`, `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all runtime input parsing, schema definitions, and payload verification in shared and client-facing packages.

### Rules

- **R-MOD-001** MUST: The consumer MUST discover the ecosystem lock or resolution artifact to determine and adhere to the exact resolved library version before utilizing validation APIs.
- **R-MOD-002** MUST: Derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-MOD-003** MUST: Execute the lock-version grounding sequence (find dependency manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for that exact version, confirm APIs exist, re-run per dependency at point of use) before writing code that uses a versioned library.
- **R-MOD-004** MUST: Compose complex validations by piping modular checks into base schemas rather than importing monolithic utility suites.
- **R-MOD-005** MUST: Ensure all schema parsing logic handles failure states uniformly at runtime boundaries.

### Verify

```bash
# Discover and run the repository verification scripts that validate module imports and runtime parsing test suites.
# Inspect module resolution outputs to verify that only modular validation primitives are bundled into target artifacts.
```

**Accept when:**
- All schema validation implementations execute runtime parsing through the designated modular validation entry point.
- Repository verification scripts confirm schema validation tests pass without unapproved monolithic validator imports.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>