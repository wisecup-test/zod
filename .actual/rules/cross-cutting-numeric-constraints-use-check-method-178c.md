---
version: 2
name: cross-cutting-numeric-constraints-use-check-method-178c
description: "Adoption of @zod/mini for Modular Schema Validation: Numeric Constraints Use Check Method Combining"
metadata:
  actual:
    adr_id: 178c03eb-c362-4d77-838a-ca11cd934771
    status: accepted
    candidate_group_id: 19ba1074-3608-4fc6-9490-5ff43e413b98
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/internal-types/**
---

# Adoption of @zod/mini for Modular Schema Validation: Numeric Constraints Use Check Method Combining

Scope: applies to `packages/integration/fixtures/internal-types/**`.

These rules are ALWAYS ACTIVE for modules defining runtime schema validation contracts, data transfer object validation, or type integrity boundaries, and internal types and integration testing fixtures verifying dual module runtime compatibility.

### Rules

- **R-ZOD-001** SHOULD: Numeric constraints SHOULD use the check method combining validation predicates rather than unconstrained primitive types.
- **R-ZOD-002** MANDATORY: Discover the project test execution script and run it to evaluate schema validation suite passes.
- **R-ZOD-003** MANDATORY: Discover the project type check script and ensure static type inference aligns with runtime schemas.
- **R-ZOD-004** MANDATORY: Discover the project module build verification script and run it across all supported module targets.

### Verify

```bash
# Discover and run the project test execution script
# Discover and run the project type check script
# Discover and run the project module build verification script across all supported module targets
```

**Accept when:**
- All schema validation test fixtures execute without parsing errors under both ECMAScript and CommonJS module formats.
- Static type checking completes with zero diagnostic errors across all schema definitions and inferred types.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>