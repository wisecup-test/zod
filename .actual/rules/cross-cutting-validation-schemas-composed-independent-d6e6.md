---
version: 2
name: cross-cutting-validation-schemas-composed-independent-d6e6
description: "Valibot Schema Validation Adoption: Validation Schemas Composed Independent Modular Schema"
metadata:
  actual:
    adr_id: d6e6c217-ec1a-44ff-9d7f-65a2130ad2d8
    status: accepted
    candidate_group_id: dc6286a1-b983-49d4-82ec-9f40035aa215
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Valibot Schema Validation Adoption: Validation Schemas Composed Independent Modular Schema

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for modules defining data schemas, input parsing, runtime boundary validation, and components requiring modular schema verification and tree-shakeable packaging.

### Rules

- **R-VAL-001** MUST: Validation schemas MUST be composed using independent modular schema functions rather than monolithic namespace objects to ensure dead-code elimination.

### Verify

```bash
# Discover and execute the project test runner configuration from the repository manifest
# Discover and run the static analysis and type verification script from the repository manifest
# Discover and execute the build bundle inspection script from repository configuration
```

**Accept when:**
- All schema validation test suites execute and pass without validation or runtime errors.
- Static type checking completes with zero type errors for all inferred schema types.
- Bundle inspection confirms unused validation functions are eliminated from production output.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline running test suites and bundle size checks, static analysis, type checking, and peer review enforce these rules.
</enforcement>