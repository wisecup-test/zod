---
version: 2
name: cross-cutting-before-integrating-updating-dependencies-283a
description: "Internal Core Module Architecture for Schema Engine and Processing Subsystems: Before Integrating Updating Dependencies Consumer Inspect"
metadata:
  actual:
    adr_id: 283a69d1-162f-46a1-9785-f59d76ae4723
    status: accepted
    candidate_group_id: 6af386df-1645-4617-9e12-ca356ef23697
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Architecture for Schema Engine and Processing Subsystems: Before Integrating Updating Dependencies Consumer Inspect

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** MUST: Before integrating or updating dependencies, the consumer MUST inspect the repository lock artifact to verify the exact resolved version against declared manifest ranges.

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
Claude Code MUST NOT skip or defer verification.
</enforcement>