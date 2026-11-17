---
version: 2
name: cross-cutting-core-library-modules-not-import-1b4a
description: "Internal Core Module Architecture for Schema Engine and Processing Subsystems: Core Library Modules Not Import Peripheral"
metadata:
  actual:
    adr_id: 1b4ae3a1-0a08-48e3-a01f-caa4a0a6e3ff
    status: accepted
    candidate_group_id: 6af386df-1645-4617-9e12-ca356ef23697
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Architecture for Schema Engine and Processing Subsystems: Core Library Modules Not Import Peripheral

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for internal library modules implementing core schema primitives, registries, error handlers, and utility routines, as well as compiler and format conversion subsystems interacting with foundational schema models.

### Rules

- **R-CORE-001** MUST_NOT: Core library modules MUST NOT import peripheral format-specific transformation modules or external parser extensions, preventing circular dependencies.

### Verify

```bash
# Run the project test suite to verify internal core module boundaries and schema compilation passes
# Execute repository linting and module boundary checks to ensure no circular imports or disallowed core module references exist
# Execute the project typechecker to confirm strict type safety across core schema exports and registry interfaces
```

**Accept when:**
- All internal module boundary tests and schema validation suites pass without errors.
- Dependency and type validation checks complete with zero circular reference or boundary violations.
- Runtime compilation methods match baseline parser behavior for all defined schema inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>