---
version: 2
name: cross-cutting-peripheral-modules-encapsulate-locale-sp-625a
description: "Internal Core Module for Shared Validation Primitives: Peripheral Modules Encapsulate Locale Specific Formatting"
metadata:
  actual:
    adr_id: 625a94f0-a311-4c80-aef3-80ab4cfa34c3
    status: accepted
    candidate_group_id: 6f1a4916-3848-4f86-b843-16c190a6b899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module for Shared Validation Primitives: Peripheral Modules Encapsulate Locale Specific Formatting

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** MAY: Peripheral modules MAY encapsulate locale-specific formatting rules provided that standardized error structures from the core module are preserved.
- **R-CORE-002** MANDATORY: Newly authored localization dictionaries MUST import error definitions and validation checks exclusively from the core module namespace.
- **R-CORE-003** MANDATORY: The consumer MUST derive tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-CORE-004** MANDATORY: Execute the lock-version grounding process in order before writing code that uses a versioned library: find dependency manifest, identify build tool, inspect repository lock/resolution artifact, look up official documentation for that exact version, confirm API existence, and re-verify per dependency at point of use.
- **R-CORE-005** MANDATORY: Imported core utility methods and visitor contracts MUST preserve backward compatibility when extending schema traversal logic.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute static analysis to validate module import paths.
# Discover and run the project test suite to verify that all localization and compatibility modules satisfy core module interface contracts.
```

**Accept when:**
- Static analysis confirms zero circular dependencies and verifies all peripheral modules import shared primitives from the internal core module.
- All automated test suites pass without interface contract mismatches or unhandled validation errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks validate static import boundaries, and pull requests violating inward module boundaries are blocked.
</enforcement>