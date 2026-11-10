---
version: 2
name: cross-cutting-schema-declarations-enforce-explicit-typ-4958
description: "Valibot Schema Validation Adoption: Schema Declarations Enforce Explicit Type Inference"
metadata:
  actual:
    adr_id: 49582e74-c423-4329-989f-02a8506d6fbf
    status: accepted
    candidate_group_id: dc6286a1-b983-49d4-82ec-9f40035aa215
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Valibot Schema Validation Adoption: Schema Declarations Enforce Explicit Type Inference

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for modules defining data schemas, input parsing, and runtime boundary validation, and components requiring modular schema verification and tree-shakeable packaging.

### Rules

- **R-VAL-001** SHOULD: Schema declarations SHOULD enforce explicit type inference derived directly from schema constructs across module interfaces.
- **R-VAL-002** MANDATORY: Import individual schema and validation primitives directly from the modular library namespace rather than re-exporting broad utility umbrellas.
- **R-VAL-003** MANDATORY: Derive static types directly from schema definitions using inferred type utilities to maintain synchronization between runtime constraints and compile-time types.

### Verify

```bash
# Discover and execute the project test runner configuration from the repository manifest
# Discover and execute the static analysis and type verification script
# Discover and execute the build bundle inspection script
```

**Accept when:**
- All schema validation test suites execute and pass without validation or runtime errors.
- Static type checking completes with zero type errors for all inferred schema types.
- Bundle inspection confirms unused validation functions are eliminated from production output.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>