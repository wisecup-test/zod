---
version: 2
name: cross-cutting-developers-inspect-repository-dependency-b10f
description: "Zod Library External Module Interface Boundary: Developers Inspect Repository Dependency Lock Artifact"
metadata:
  actual:
    adr_id: b10f2f45-79ca-421f-b257-ca88e57eeb39
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

# Zod Library External Module Interface Boundary: Developers Inspect Repository Dependency Lock Artifact

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all public distribution entrypoints, package export targets, and module interface boundary definitions for the Zod library.

### Rules

- **R-ZOD-001** MUST: Developers MUST inspect the repository dependency lock artifact to determine the exact resolved version of any versioned dependency before authoring or modifying interface bindings.

### Verify

```bash
# Discover and run the repository interface validation and type check scripts
# Discover and run the project test suite
```

**Accept when:**
- All distribution entrypoint exports pass repository interface and type validation checks without boundary violations.
- All public interface contract test suites pass successfully across all distribution variants.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration type checking, boundary linting, and peer code review audit all modifications to package entrypoints and external interface boundary modules.
</enforcement>