---
version: 2
name: cross-cutting-localization-modules-format-error-messag-e75d
description: "ZodError Centralized Validation Error Representation Architecture: Localization Modules Format Error Messages Strictly"
metadata:
  actual:
    adr_id: e75d4988-da65-44f4-94fd-3a95a2ab7d44
    status: accepted
    candidate_group_id: 2a760602-eb59-42b6-93ff-193614615ecc
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# ZodError Centralized Validation Error Representation Architecture: Localization Modules Format Error Messages Strictly

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for schema parsing, validation execution pipelines, validation error message localization and formatting modules, and core error representation and issue construction helper modules.

### Rules

- **R-ZOD-001** MUST: Localization modules MUST format error messages strictly against standardized issue descriptors defined by ZodError without introducing independent error representation schemas.
- **R-ZOD-002** MUST: Follow the lock-version grounding policy: find the dependency manifest, identify the build tool, inspect the repository lock or resolution artifact to determine the exact resolved version, and confirm every API or function exists in that version's documentation before use.
- **R-ZOD-003** MUST: Keep shared utility modules side-effect-free to ensure safe consumption across both parsing and localization layers.
- **R-ZOD-004** MUST: Ensure localization formatters consume structured issue descriptors rather than raw parser internal state to maintain loose coupling.

### Verify

```bash
# Discover and run the test runner defined in project configuration covering parsing utilities and error localization
# Discover and run the static analysis/type checking script to verify module import resolution and type consistency
# Inspect dependency resolution artifact to confirm module imports align with declared dependency boundaries
```

**Accept when:**
- All schema parsing and localization test suites pass without validation issue schema mismatches.
- Automated static type verification passes with zero type errors across module boundaries consuming ZodError and shared utility functions.
- Validation error emissions consistently conform to the standardized issue descriptors defined by ZodError across all configured locales.

<enforcement>
Claude Code MUST NOT skip or defer verification. All error constructions must adhere to ZodError type definitions, and pull requests introducing unstandardized error shapes or bypassing centralized error utilities are blocked.
</enforcement>