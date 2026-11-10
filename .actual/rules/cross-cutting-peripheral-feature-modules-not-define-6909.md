---
version: 2
name: cross-cutting-peripheral-feature-modules-not-define-6909
description: "Internal Core Module for Shared Validation Primitives: Peripheral Feature Modules Not Define Standalone"
metadata:
  actual:
    adr_id: 6909613a-65db-497f-b98b-eb5b8a5742e0
    status: accepted
    candidate_group_id: 6f1a4916-3848-4f86-b843-16c190a6b899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module for Shared Validation Primitives: Peripheral Feature Modules Not Define Standalone

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all localization dictionaries, schema adapters, compatibility translation layers, and peripheral extensions requiring shared validation checks or error structures.

### Rules

- **R-CORE-001** MUST_NOT: Peripheral feature modules MUST NOT define standalone error representations or duplicate foundational validation check routines that already exist within the core module.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute static analysis to validate module import paths
# Discover and run the project test suite to verify that all localization and compatibility modules satisfy core module interface contracts
```

**Accept when:**
- Static analysis confirms zero circular dependencies and verifies all peripheral modules import shared primitives from the internal core module.
- All automated test suites pass without interface contract mismatches or unhandled validation errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration builds fail upon detection of unauthorized dependency paths or duplicate validation primitives, and pull requests violating inward module boundaries are blocked until refactored.
</enforcement>