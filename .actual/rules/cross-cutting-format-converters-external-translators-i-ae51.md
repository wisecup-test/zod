---
version: 2
name: cross-cutting-format-converters-external-translators-i-ae51
description: "Internal Core Module Architecture for Schema Engine and Processing Subsystems: Format Converters External Translators Interact Core"
metadata:
  actual:
    adr_id: ae5143f9-f6fd-42f3-9f62-1ccde1312e75
    status: accepted
    candidate_group_id: 6af386df-1645-4617-9e12-ca356ef23697
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Architecture for Schema Engine and Processing Subsystems: Format Converters External Translators Interact Core

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for internal library modules implementing core schema primitives, registries, error handlers, and utility routines, as well as compiler and format conversion subsystems interacting with foundational schema models.

### Rules

- **R-CORE-001** MUST: Format converters and external translators MUST interact with core schema representations strictly through core library module interfaces and registry accessors.

### Verify

```bash
# Run the project test suite to verify internal core module boundaries and schema compilation passes
# Execute the repository linting and module boundary checks to ensure no circular imports or disallowed core module references exist
# Execute the project typechecker to confirm strict type safety across core schema exports and registry interfaces
```

**Accept when:**
- All internal module boundary tests and schema validation suites pass without errors.
- Dependency and type validation checks complete with zero circular reference or boundary violations.
- Runtime compilation methods match baseline parser behavior for all defined schema inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>