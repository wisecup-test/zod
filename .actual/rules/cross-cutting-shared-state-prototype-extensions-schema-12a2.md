---
version: 2
name: cross-cutting-shared-state-prototype-extensions-schema-12a2
description: "Internal Core Module Architecture for Schema Engine and Processing Subsystems: Shared State Prototype Extensions Schema Reference"
metadata:
  actual:
    adr_id: 12a207e8-b43a-4cb5-b8eb-97488bf9d392
    status: accepted
    candidate_group_id: 6af386df-1645-4617-9e12-ca356ef23697
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Architecture for Schema Engine and Processing Subsystems: Shared State Prototype Extensions Schema Reference

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for internal library modules implementing core schema primitives, registries, error handlers, and utility routines, as well as compiler and format conversion subsystems interacting with foundational schema models.

### Rules

- **R-CORE-001** MUST: Shared state, prototype extensions, and schema reference mappings MUST be managed through dedicated registry instances and contextual tracking objects to prevent cross-validation pollution.

### Verify

```bash
# Run the project test suite to verify internal core module boundaries and schema compilation passes
# Execute repository linting and module boundary checks
# Execute project typechecker to confirm strict type safety across core schema exports and registry interfaces
```

**Accept when:**
- All internal module boundary tests and schema validation suites pass without errors.
- Dependency and type validation checks complete with zero circular reference or boundary violations.
- Runtime compilation methods match baseline parser behavior for all defined schema inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Static module boundary analysis, peer reviews, and automated unit/integration tests enforce these rules.
</enforcement>