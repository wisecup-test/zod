---
version: 2
name: cross-cutting-schema-parsing-utilities-error-localizat-f021
description: "ZodError Centralized Validation Error Representation Architecture: Schema Parsing Utilities Error Localization Modules"
metadata:
  actual:
    adr_id: f0216996-ef5f-4156-b29d-f254d01c740e
    status: accepted
    candidate_group_id: 2a760602-eb59-42b6-93ff-193614615ecc
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# ZodError Centralized Validation Error Representation Architecture: Schema Parsing Utilities Error Localization Modules

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for:
- Schema parsing and validation execution pipelines.
- Validation error message localization and formatting modules.
- Core error representation and issue construction helper modules.

### Rules

- **R-LM-001** MUST: All schema parsing utilities and error localization modules MUST import and use ZodError as the unified representation for validation issue types and error data structures.

### Verify

- Discover the test runner defined in the project configuration manifest and execute the test suite covering parsing utilities and error localization.
- Discover the static analysis and type checking script configured in the project repository and run it to verify module import resolution and type consistency across core error modules.
- Inspect the project dependency resolution artifact to confirm all module imports align with declared dependency boundaries.

**Accept when:**

- All schema parsing and localization test suites pass without validation issue schema mismatches.
- Automated static type verification passes with zero type errors across module boundaries consuming ZodError and shared utility functions.
- Validation error emissions consistently conform to the standardized issue descriptors defined by ZodError across all configured locales.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static type analysis verifying that all error constructions adhere to ZodError type definitions.
- Verified by: Continuous integration test suites verifying issue formatting and locale message generation across parsing routines.
- Verified by: Peer code review verifying that new parsing utilities do not introduce ad-hoc error structures.
- Violation handling: Pull requests introducing unstandardized error shapes or bypassing centralized error utilities are rejected.
- Violation handling: Static analysis failures on incompatible error issue structures block integration pipelines.
- Exception process: Exceptions to centralized error issue representation require architectural review and formal approval by the core maintainers.
- Exception process: Any approved deviation must be accompanied by dedicated regression tests verifying compatibility with standard error handling consumers.
</enforcement>
