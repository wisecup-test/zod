---
version: 2
name: cross-cutting-feature-modules-defining-localization-ma-eafa
description: "Internal Core Module for Shared Validation Primitives: Feature Modules Defining Localization Mappings Compatibility"
metadata:
  actual:
    adr_id: eafaa2c8-9ab0-4a9e-9d91-2936e3230d8f
    status: accepted
    candidate_group_id: 6f1a4916-3848-4f86-b843-16c190a6b899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module for Shared Validation Primitives: Feature Modules Defining Localization Mappings Compatibility

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all feature modules defining localization mappings or compatibility schemas.

### Rules

- **R-CORE-001** MUST: Feature modules defining localization mappings or compatibility schemas MUST consume validation checks, error representations, visitor traversals, and shared utilities directly from the internal core module.

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