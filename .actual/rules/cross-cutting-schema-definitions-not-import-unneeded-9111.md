---
version: 2
name: cross-cutting-schema-definitions-not-import-unneeded-9111
description: "Valibot Schema Validation Adoption: Schema Definitions Not Import Unneeded Validation"
metadata:
  actual:
    adr_id: 9111f16a-6b0d-416a-9404-852436f546c6
    status: accepted
    candidate_group_id: dc6286a1-b983-49d4-82ec-9f40035aa215
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Valibot Schema Validation Adoption: Schema Definitions Not Import Unneeded Validation

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for modules defining data schemas, input parsing, and runtime boundary validation, excluding internal language-primitive manipulations and performance-critical inner loops where formal schema boundaries are not exposed (unless covered by exception EXC-20-001).

### Rules

- **R-VAL-001** MUST_NOT: Schema definitions MUST NOT import unneeded validation functions or bundle entire library namespaces into runtime bundles.

### Verify

```bash
# Discover and execute the validation test suite from project manifest
# Discover and run static analysis and type verification script
# Discover and execute build bundle inspection script to verify modular tree-shaking compliance
```

**Accept when:**
- All schema validation test suites execute and pass without validation or runtime errors.
- Static type checking completes with zero type errors for all inferred schema types.
- Bundle inspection confirms unused validation functions are eliminated from production output.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory for all schema validation updates.
</enforcement>