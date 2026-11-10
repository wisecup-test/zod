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

These rules are ALWAYS ACTIVE for all public distribution entrypoints, package export targets, and module interface boundary definitions across library variants for the Zod library.

### Rules

- **R-ZOD-001** MAY: Module variants targeting constrained environments MAY exclude non-critical secondary utilities from their re-exported external surface while preserving core interface contracts.
- **R-ZOD-002** MANDATORY (DISCOVERY POLICY): Consumer MUST discover dependency manifest, build tool, and repository lock/resolution artifacts from the repository.
- **R-ZOD-003** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock/resolution artifact for exact version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps 3-5 per dependency at point of use for version-sensitive behavior.
- **R-ZOD-004** MANDATORY: Maintainers must channel new public API capabilities through the designated external interface boundary module rather than directly exposing internal implementation structures.
- **R-ZOD-005** MANDATORY: Verify that all distribution entrypoints import and re-export the unified external module to avoid accidental divergence in public contract definitions.

### Verify

```bash
# Discover and run repository interface validation, type check scripts, and test suite
npm run test
npm run typecheck
```

**Accept when:**
- All distribution entrypoint exports pass repository interface and type validation checks without boundary violations.
- All public interface contract test suites pass successfully across all distribution variants.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration type checking, boundary linting, and peer code review auditing are mandatory.
</enforcement>