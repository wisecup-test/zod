---
version: 2
name: cross-cutting-internal-schema-validation-compilation-s-06e0
description: "Internal Core Module Architecture for Schema Engine and Processing Subsystems: Internal Schema Validation Compilation Subsystems Isolate"
metadata:
  actual:
    adr_id: 06e0e16b-534e-46f1-a51a-a0a155e2d245
    status: accepted
    candidate_group_id: 6af386df-1645-4617-9e12-ca356ef23697
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Architecture for Schema Engine and Processing Subsystems: Internal Schema Validation Compilation Subsystems Isolate

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** MUST: Internal schema validation and compilation subsystems MUST isolate foundational schema definitions, validation checks, registries, and error primitives within dedicated core library modules rather than coupling them directly to format conversion or external API adapters.

### Verify

```bash
# Run the project test suite to verify internal core module boundaries and schema compilation passes all functional suites.
# Execute the repository linting and module boundary checks to ensure no circular imports or disallowed core module references exist.
# Execute the project typechecker to confirm strict type safety across core schema exports and registry interfaces.
```

**Accept when:**
- All internal module boundary tests and schema validation suites pass without errors.
- Dependency and type validation checks complete with zero circular reference or boundary violations.
- Runtime compilation methods match baseline parser behavior for all defined schema inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via static module boundary analysis, peer review, and automated unit/integration test coverage.
</enforcement>