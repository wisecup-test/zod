---
version: 2
name: cross-cutting-package-entrypoints-exposing-zod-public-dd86
description: "Zod Library External Module Interface Boundary: Package Entrypoints Exposing Zod Public Interface"
metadata:
  actual:
    adr_id: dd86f2cc-2491-4710-b471-7b3032c981da
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

# Zod Library External Module Interface Boundary: Package Entrypoints Exposing Zod Public Interface

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all public distribution entrypoints and package export targets for the Zod library.

### Rules

- **R-ZOD-001** MUST: Package entrypoints exposing the Zod public interface MUST route all external surface exports through a dedicated external boundary module rather than exposing internal core implementations directly.

### Verify

```bash
# Discover and run the repository interface validation and type check scripts to verify module boundary conformance.
# Discover and run the project test suite to verify that all distribution entrypoint exports satisfy expected public contract behaviors.
```

**Accept when:**
- All distribution entrypoint exports pass repository interface and type validation checks without boundary violations.
- All public interface contract test suites pass successfully across all distribution variants.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration type checking and boundary linting scripts discovered from repository configurations must pass successfully, and peer code review must audit all modifications to package entrypoints and external interface boundary modules.
</enforcement>