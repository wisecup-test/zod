---
version: 2
name: cross-cutting-interactions-between-peripheral-feature-8cec
description: "Internal Core Module for Shared Validation Primitives: Interactions Between Peripheral Feature Modules Internal"
metadata:
  actual:
    adr_id: 8cecb3c4-4576-4d82-baad-599c8488767f
    status: accepted
    candidate_group_id: 6f1a4916-3848-4f86-b843-16c190a6b899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module for Shared Validation Primitives: Interactions Between Peripheral Feature Modules Internal

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all localization dictionaries, schema adapters, compatibility translation layers, and peripheral extensions requiring shared validation checks or error structures.

### Rules

- **R-INT-001** SHOULD: Interactions between peripheral feature modules and internal core submodules SHOULD be restricted to exposed interfaces for checks, errors, utilities, and visitor traversals.
- **R-INT-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-INT-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run per dependency at point of use for version-sensitive behavior.
- **R-INT-004** MANDATORY: Newly authored localization dictionaries MUST import error definitions and validation checks exclusively from the core module namespace.
- **R-INT-005** MANDATORY: All imported core utility methods and visitor contracts MUST preserve backward compatibility when extending schema traversal logic.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute static analysis to validate module import paths.
# Discover and run the project test suite to verify that all localization and compatibility modules satisfy core module interface contracts.
```

**Accept when:**
- Static analysis confirms zero circular dependencies and verifies all peripheral modules import shared primitives from the internal core module.
- All automated test suites pass without interface contract mismatches or unhandled validation errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration builds fail upon detection of unauthorized dependency paths or duplicate validation primitives.
</enforcement>