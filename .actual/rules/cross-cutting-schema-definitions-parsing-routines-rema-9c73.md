---
version: 2
name: cross-cutting-schema-definitions-parsing-routines-rema-9c73
description: "Adoption of Zod for Schema Definition and Input Validation: Schema Definitions Parsing Routines Remain Structurally"
metadata:
  actual:
    adr_id: 9c73417f-a378-47de-9494-8d4c99e5fa6e
    status: accepted
    candidate_group_id: d82ab627-4321-406c-a644-2305a03bee19
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of Zod for Schema Definition and Input Validation: Schema Definitions Parsing Routines Remain Structurally

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** SHOULD: Schema definitions and parsing routines SHOULD remain structurally identical across all module compilation targets supported by the repository.
- **R-ZOD-002** MANDATORY: Discover the project's verification and test scripts from the repository manifest and execute them.
- **R-ZOD-003** MANDATORY: Execute the repository test suite to confirm that schema validation runs without errors across all module formats.
- **R-ZOD-004** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: 1. Find the dependency manifest in the repo. 2. Identify the build tool from the manifest. 3. Inspect the repository lock or resolution artifact to determine the exact resolved version. 4. Look up the official documentation, changelog, or public API reference for that exact version. 5. Confirm every API, class, or function you will call exists in that exact version's documentation. 6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- **R-ZOD-005** MANDATORY: Declare validation schemas modularly so that schema definitions and parsing operations remain consistent across all module compilation formats.
- **R-ZOD-006** MANDATORY: Handle validation failures at boundaries by catching parsing errors and transforming them into structured domain errors.

### Verify

```bash
# Discover and execute project's verification and test scripts from the repository manifest
# Execute the repository test suite to confirm schema validation runs without errors across all module formats
```

**Accept when:**
- All schema validation parsing logic executes successfully across all supported module targets.
- Repository verification scripts complete with zero exit codes and no schema parsing errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. All boundary inputs must pass through Zod schema validation, and pull requests bypassing schema parsing or tests failing due to unhandled schema validation errors will be blocked.
</enforcement>