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

These rules are ALWAYS ACTIVE for:
- Internal library modules implementing core schema primitives, registries, error handlers, and utility routines.
- Compiler and format conversion subsystems interacting with foundational schema models.

### Rules

- **R-LM-001** MUST: Shared state, prototype extensions, and schema reference mappings MUST be managed through dedicated registry instances and contextual tracking objects to prevent cross-validation pollution.

### Verify

- Run the project test suite to verify internal core module boundaries and schema compilation passes all functional suites.
- Execute the repository linting and module boundary checks to ensure no circular imports or disallowed core module references exist.
- Execute the project typechecker to confirm strict type safety across core schema exports and registry interfaces.

**Accept when:**

- All internal module boundary tests and schema validation suites pass without errors.
- Dependency and type validation checks complete with zero circular reference or boundary violations.
- Runtime compilation methods match baseline parser behavior for all defined schema inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Static module boundary analysis in the continuous integration pipeline.
- Verified by: Peer review focusing on dependency direction between core modules and peripheral adapters.
- Verified by: Automated unit and integration test coverage across schema processing layers.
- Violation handling: Pull requests introducing circular dependencies between core modules and external adapters will be rejected.
- Violation handling: Non-compliant direct access to internal schema structures bypassing registry accessors must be refactored prior to merge.
- Exception process: Exceptions require architectural review and explicit sign-off by library maintainers with documented justification and remediation plans.
</enforcement>
