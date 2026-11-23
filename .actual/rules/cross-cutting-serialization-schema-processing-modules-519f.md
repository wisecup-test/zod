---
version: 2
name: cross-cutting-serialization-schema-processing-modules-519f
description: "Internal Core Library Module Decomposition and Registry Pattern in Zod: Serialization Schema Processing Modules Not Introduce"
metadata:
  actual:
    adr_id: 519f1c3a-62be-4856-8485-f34a8a856c8f
    status: accepted
    candidate_group_id: fd8d8f66-6b2f-4c03-8911-bd9f1e5e7e6f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Internal Core Library Module Decomposition and Registry Pattern in Zod: Serialization Schema Processing Modules Not Introduce

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for:
- All internal modules within the core library package responsible for schema definitions, validation checks, registry lookups, and schema transformations.
- Functions performing recursive schema graph analysis, serialization, or metadata aggregation.

### Rules

- **R-LM-001** MUST_NOT: Serialization and schema processing modules MUST NOT introduce circular import dependencies into core schema definition and validation check modules.

### Verify

- Discover and execute the repository test runner to validate recursive schema generation, registry lookups, and serialization behaviors.
- Discover and execute the repository module boundary and circular dependency verification scripts to ensure import isolation between core submodules.
- Discover and execute the repository static type checker to verify internal interface compatibility across all core module boundaries.

**Accept when:**

- All core module interfaces and internal imports resolve through the defined module boundaries without circular module initialization errors.
- Schema transformations and serializations correctly track cyclic structures using the contextual traversal cache without memory leaks.
- Static type checking and automated regression suites pass completely across all core library components.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis and module boundary linting executed during continuous integration.
- Verified by: Mandatory peer code review by core library maintainers focusing on internal import hierarchies and context propagation.
- Verified by: Comprehensive unit and integration test suites validating recursive schema transformation and cycle detection behavior.
- Violation handling: Pull requests containing direct circular module imports or bypassed registry context structures are blocked from merging.
- Violation handling: Code review rejections require refactoring non-compliant internal modules to align with designated module boundaries and context protocols.
- Exception process: Submit an architectural exception request detailing the structural constraints that preclude using standard internal core modules or registry context traversal.
- Exception process: Obtain formal approval from core library maintainers prior to merging any alternative state passing or module coupling pattern.
</enforcement>
