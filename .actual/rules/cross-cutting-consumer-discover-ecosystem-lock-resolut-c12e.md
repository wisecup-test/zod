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

- **R-ADR-001** MUST: The consumer MUST discover the ecosystem lock or resolution artifact to determine and adhere to the exact resolved library version before utilizing validation APIs.
- **R-ADR-002** MUST: Execute in order before writing code that uses a versioned library: (1) Find the dependency manifest in the repo, (2) Identify the build tool from the manifest, (3) Inspect the repository lock or resolution artifact to determine the exact resolved version, (4) Look up the official documentation, changelog, or public API reference for that exact version, (5) Confirm every API, class, or function you will call exists in that exact version's documentation, (6) For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- **R-ADR-003** MUST: Compose complex validations by piping modular checks into base schemas rather than importing monolithic utility suites.
- **R-ADR-004** MUST: Ensure all schema parsing logic handles failure states uniformly at runtime boundaries.

### Verify

```bash
# Discover and run repository verification scripts that validate module imports and runtime parsing test suites
# Inspect module resolution outputs to verify that only modular validation primitives are bundled into target artifacts
```

**Accept when:**
- All schema validation implementations execute runtime parsing through the designated modular validation entry point.
- Repository verification scripts confirm schema validation tests pass without unapproved monolithic validator imports.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, module import inspection, and code review verification will flag non-modular validation namespaces as blocking lint or static analysis violations.
</enforcement>