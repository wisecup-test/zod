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

These rules are ALWAYS ACTIVE for:
- Internal library modules implementing core schema primitives, registries, error handlers, and utility routines.
- Compiler and format conversion subsystems interacting with foundational schema models.

### Rules

- **R-LM-001** MUST_NOT: Core library modules MUST NOT import peripheral format-specific transformation modules or external parser extensions, preventing circular dependencies.

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
