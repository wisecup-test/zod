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

These rules are ALWAYS ACTIVE for:
- All runtime input parsing, schema definitions, and payload verification in shared and client-facing packages.

### Rules

- **R-LM-001** MUST: The consumer MUST discover the ecosystem lock or resolution artifact to determine and adhere to the exact resolved library version before utilizing validation APIs.

### Verify

- Discover and run the repository verification scripts that validate module imports and runtime parsing test suites.
- Inspect module resolution outputs to verify that only modular validation primitives are bundled into target artifacts.

**Accept when:**

- All schema validation implementations execute runtime parsing through the designated modular validation entry point.
- Repository verification scripts confirm schema validation tests pass without unapproved monolithic validator imports.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis and module import inspection in continuous integration workflows.
- Verified by: Code review verification of schema definition patterns and parsing calls.
- Violation handling: Flag imports of non-modular validation namespaces as blocking lint or static analysis violations.
- Violation handling: Require refactoring of direct manual validation assertions into standardized modular schema definitions.
- Exception process: Submit an architectural review request documenting technical constraints that necessitate alternative schema validation mechanisms.
- Exception process: Obtain sign-off from module owners prior to introducing external schema parsers.
</enforcement>
