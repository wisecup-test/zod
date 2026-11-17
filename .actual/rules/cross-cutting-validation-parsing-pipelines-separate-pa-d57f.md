---
version: 2
name: cross-cutting-validation-parsing-pipelines-separate-pa-d57f
description: "ZodError Centralized Validation Error Representation Architecture: Validation Parsing Pipelines Separate Parse Result"
metadata:
  actual:
    adr_id: d57f69de-2d24-4dcd-87df-1ccbec1c1cc9
    status: accepted
    candidate_group_id: 2a760602-eb59-42b6-93ff-193614615ecc
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# ZodError Centralized Validation Error Representation Architecture: Validation Parsing Pipelines Separate Parse Result

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for schema parsing and validation execution pipelines, validation error message localization and formatting modules, and core error representation and issue construction helper modules.

### Rules

- **R-VAL-001** SHOULD: Validation parsing pipelines SHOULD separate parse result state tracking from localized message string synthesis.
- **R-VAL-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-VAL-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact resolved version, look up official documentation for that exact version, and confirm every API/class/function exists in that version before using it.
- **R-VAL-004** MANDATORY: Shared utility modules must contain side-effect-free helper routines to ensure safe consumption across both parsing and localization layers.
- **R-VAL-005** MANDATORY: Localization formatters must consume structured issue descriptors rather than raw parser internal state to maintain loose coupling.

### Verify

```bash
# Discover and execute the test runner defined in the project configuration manifest covering parsing utilities and error localization
# Discover and run the static analysis and type checking script configured in the project repository to verify module import resolution and type consistency
# Inspect the project dependency resolution artifact to confirm all module imports align with declared dependency boundaries
```

**Accept when:**
- All schema parsing and localization test suites pass without validation issue schema mismatches.
- Automated static type verification passes with zero type errors across module boundaries consuming ZodError and shared utility functions.
- Validation error emissions consistently conform to the standardized issue descriptors defined by ZodError across all configured locales.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static type analysis verifying that all error constructions adhere to ZodError type definitions, continuous integration test suites verifying issue formatting and locale message generation across parsing routines, and peer code review verifying that new parsing utilities do not introduce ad-hoc error structures.
</enforcement>