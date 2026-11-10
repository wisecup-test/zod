---
version: 2
name: cross-cutting-core-module-primitives-not-establish-5374
description: "Internal Core Module for Shared Validation Primitives: Core Module Primitives Not Establish Circular"
metadata:
  actual:
    adr_id: 5374661b-8b9e-480c-a5e9-66e8d7d72541
    status: accepted
    candidate_group_id: 6f1a4916-3848-4f86-b843-16c190a6b899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module for Shared Validation Primitives: Core Module Primitives Not Establish Circular

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all localization dictionaries, schema adapters, compatibility translation layers, and peripheral extensions requiring shared validation checks or error structures.

### Rules

- **R-CORE-001** MUST_NOT: Core module primitives MUST NOT establish circular or outward dependencies onto the peripheral feature modules that consume them.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute static analysis to validate module import paths.
# Discover and run the project test suite to verify that all localization and compatibility modules satisfy core module interface contracts.
```

**Accept when:**
- Static analysis confirms zero circular dependencies and verifies all peripheral modules import shared primitives from the internal core module.
- All automated test suites pass without interface contract mismatches or unhandled validation errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory and enforced by continuous integration checks validating static import boundaries and automated test suites.
</enforcement>