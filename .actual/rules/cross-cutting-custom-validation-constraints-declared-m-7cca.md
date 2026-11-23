---
version: 2
name: cross-cutting-custom-validation-constraints-declared-m-7cca
description: "Adoption of zod/mini for Modular Schema Definition and Input Validation: Custom Validation Constraints Declared Modular Check"
metadata:
  actual:
    adr_id: 7ccaa146-eb38-475f-aef8-37a45cc3d7bb
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

# Adoption of zod/mini for Modular Schema Definition and Input Validation: Custom Validation Constraints Declared Modular Check

Scope: applies to `packages/bench/**`, `packages/resolution/src/**`, `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for:
- All runtime input parsing, schema definitions, and payload verification in shared and client-facing packages.

### Rules

- **R-LM-001** SHOULD: Custom validation constraints SHOULD be declared using modular check functions attached to base type schemas.

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
