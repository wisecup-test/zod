---
version: 2
name: cross-cutting-module-variants-targeting-constrained-en-9d9e
description: "Zod Library External Module Interface Boundary: Module Variants Targeting Constrained Environments Exclude"
metadata:
  actual:
    adr_id: 9d9eeb11-cdb9-40cb-bbd8-e2bf9dc28eff
    status: accepted
    candidate_group_id: f81b1c2a-31a4-4cd6-90ee-06cb363b9402
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
      - src/v4/**
---

# Zod Library External Module Interface Boundary: Module Variants Targeting Constrained Environments Exclude

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for:
- Applies to all public distribution entrypoints and package export targets for the Zod library.
- Applies when defining or refactoring public module interface boundaries across library variants.

### Rules

- **R-LM-001** MAY: Module variants targeting constrained environments MAY exclude non-critical secondary utilities from their re-exported external surface while preserving core interface contracts.

### Verify

- Discover and run the repository interface validation and type check scripts to verify module boundary conformance.
- Discover and run the project test suite to verify that all distribution entrypoint exports satisfy expected public contract behaviors.

**Accept when:**

- All distribution entrypoint exports pass repository interface and type validation checks without boundary violations.
- All public interface contract test suites pass successfully across all distribution variants.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Continuous integration type checking and boundary linting scripts discovered from repository configurations.
- Verified by: Peer code review auditing all modifications to package entrypoints and external interface boundary modules.
- Violation handling: Pull requests introducing direct imports of internal modules from entrypoints or bypassing external boundary modules are blocked from merging until corrected.
- Exception process: Exceptions require documented architectural justification and formal sign-off from module maintainers.
</enforcement>
