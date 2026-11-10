---
version: 2
name: cross-cutting-library-module-variants-sharing-common-47c7
description: "Zod Library External Module Interface Boundary: Library Module Variants Sharing Common External"
metadata:
  actual:
    adr_id: 47c739c0-9024-48d1-99d7-3d26470aecf8
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

# Zod Library External Module Interface Boundary: Library Module Variants Sharing Common External

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all public distribution entrypoints, package export targets, and module interface boundaries for the Zod library.

### Rules

- **R-ZOD-001** SHOULD: Library module variants sharing common external public contracts reuse the unified external boundary module to maintain consistent public API surface contracts across distributions.

### Verify

```bash
# Discover and run repository interface validation, type checking, and test scripts
npm run test
npm run typecheck
```

**Accept when:**
- All distribution entrypoint exports pass repository interface and type validation checks without boundary violations.
- All public interface contract test suites pass successfully across all distribution variants.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>