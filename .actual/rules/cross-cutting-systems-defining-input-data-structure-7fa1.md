---
version: 2
name: cross-cutting-systems-defining-input-data-structure-7fa1
description: "Valibot Schema Validation Adoption: Systems Defining Input Data Structure Validation"
metadata:
  actual:
    adr_id: 7fa137f6-a77e-41ad-bafe-0b22227a513c
    status: accepted
    candidate_group_id: dc6286a1-b983-49d4-82ec-9f40035aa215
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Valibot Schema Validation Adoption: Systems Defining Input Data Structure Validation

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all modules defining data schemas, input parsing, and runtime boundary validation.

### Rules

- **R-VAL-001** MUST: Systems defining input and data structure validation MUST adopt Valibot as the schema specification library across modular boundaries.

### Verify

```bash
# Discover the project test runner configuration from the repository manifest and execute the validation test suite.
# Discover the static analysis and type verification script from the repository manifest and run it to verify schema compilation.
# Discover the build bundle inspection script from repository configuration and execute it to verify modular tree-shaking compliance.
```

**Accept when:**
- All schema validation test suites execute and pass without validation or runtime errors.
- Static type checking completes with zero type errors for all inferred schema types.
- Bundle inspection confirms unused validation functions are eliminated from production output.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>