---
version: 2
name: cross-cutting-package-entrypoint-modules-not-import-4f1a
description: "Zod Library External Module Interface Boundary: Package Entrypoint Modules Not Import Internal"
metadata:
  actual:
    adr_id: 4f1ac79d-5c0a-4dd5-9faa-9ff91298ed11
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

# Zod Library External Module Interface Boundary: Package Entrypoint Modules Not Import Internal

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all public distribution entrypoints, package export targets, and module interface boundaries for the Zod schema library.

### Rules

- **R-ZOD-001** MUST_NOT: Package entrypoint modules MUST NOT import internal core schema constructs directly if those constructs bypass the designated external boundary module.

### Verify

```bash
# Discover and run the repository interface validation and type check scripts to verify module boundary conformance.
# Discover and run the project test suite to verify that all distribution entrypoint exports satisfy expected public contract behaviors.
```

**Accept when:**
- All distribution entrypoint exports pass repository interface and type validation checks without boundary violations.
- All public interface contract test suites pass successfully across all distribution variants.

<enforcement>
Claude Code MUST NOT skip or defer verification. All distribution entrypoints and external interface boundary modules must be audited through continuous integration type checking, boundary linting scripts, and peer code reviews.
</enforcement>