---
version: 2
name: cross-cutting-when-integrating-consuming-versioned-dep-b21f
description: "ZodError Centralized Validation Error Representation Architecture: When Integrating Consuming Versioned Dependencies Developers"
metadata:
  actual:
    adr_id: b21fe633-1a6b-4d9e-9fbf-f73e92047b74
    status: accepted
    candidate_group_id: 2a760602-eb59-42b6-93ff-193614615ecc
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# ZodError Centralized Validation Error Representation Architecture: When Integrating Consuming Versioned Dependencies Developers

Scope: applies to `packages/zod/src/v3/**`.

These rules are ALWAYS ACTIVE for all schema parsing, validation execution pipelines, validation error message localization, formatting modules, and core error representation modules.

### Rules

- **R-ZOD-001** MUST: When integrating or consuming versioned dependencies, developers MUST discover the dependency manifest and inspect the repository lock artifact to determine and enforce the exact locked version.
- **R-ZOD-002** MUST: Follow the lock-version grounding process before writing code that uses a versioned library: find the dependency manifest, identify the build tool, inspect the repository lock/resolution artifact for the exact resolved version, look up official documentation for that exact version, and confirm every API/class/function exists in that exact version before using it.
- **R-ZOD-003** MUST: Use ZodError as the unified error representation to establish a consistent contract for issue reporting across all schema validators.
- **R-ZOD-004** MUST: Route error generation through common utility helpers to prevent fragmentation of error handling behavior and simplify maintenance.
- **R-ZOD-005** MUST: Isolate locale definitions from parser internals to allow dynamic language translation without modifying parsing algorithms.
- **R-ZOD-006** MUST: Maintain strict module layering where error definitions and common utilities serve as leaf dependencies imported by parsers and locales without back-references to avoid circular dependencies.

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
Claude Code MUST NOT skip or defer verification. Automated static analysis and test suites must verify error consistency, and pull requests introducing unstandardized error shapes or bypassing centralized error utilities are rejected.
</enforcement>