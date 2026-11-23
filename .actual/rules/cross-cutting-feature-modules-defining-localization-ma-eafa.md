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

These rules are ALWAYS ACTIVE for:
- Implementation of localization dictionaries and error message mappings
- Implementation of schema adapters and compatibility translation layers
- Creation of peripheral extensions requiring shared validation checks or error structures

### Rules

- **R-LM-001** MUST: Feature modules defining localization mappings or compatibility schemas MUST consume validation checks, error representations, visitor traversals, and shared utilities directly from the internal core module.

### Verify

- Discover the project verification script from the repository manifest and execute static analysis to validate module import paths.
- Discover and run the project test suite to verify that all localization and compatibility modules satisfy core module interface contracts.

**Accept when:**

- Static analysis confirms zero circular dependencies and verifies all peripheral modules import shared primitives from the internal core module.
- All automated test suites pass without interface contract mismatches or unhandled validation errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks validating static import boundaries.
- Verified by: Peer code review for all pull requests modifying core interfaces or adding localization files.
- Violation handling: Continuous integration builds fail upon detection of unauthorized dependency paths or duplicate validation primitives.
- Violation handling: Pull requests violating inward module boundaries are blocked until refactored.
- Exception process: Submit an architectural review request detailing technical constraints preventing reliance on the core module.
- Exception process: Temporary exceptions require formal sign-off from the core architecture team with a scheduled remediation plan.
</enforcement>
