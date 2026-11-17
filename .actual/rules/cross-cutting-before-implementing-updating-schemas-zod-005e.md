---
version: 2
name: cross-cutting-before-implementing-updating-schemas-zod-005e
description: "Adoption of @zod/mini for Modular Schema Validation: Before Implementing Updating Schemas Zod Mini"
metadata:
  actual:
    adr_id: 005e9993-4ecf-48a9-821f-909e6f2d4567
    status: accepted
    candidate_group_id: 19ba1074-3608-4fc6-9490-5ff43e413b98
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/internal-types/**
---

# Adoption of @zod/mini for Modular Schema Validation: Before Implementing Updating Schemas Zod Mini

Scope: applies to `packages/integration/fixtures/internal-types/**`.

These rules are ALWAYS ACTIVE for modules defining runtime schema validation contracts, data transfer object validation, or type integrity boundaries, and internal types and integration testing fixtures verifying dual module runtime compatibility.

### Rules

- **R-ZOD-001** MUST: Before implementing or updating schemas using @zod/mini, consumers MUST inspect the repository lock or resolution artifact to confirm the exact resolved library version and align usage with its documented API surface.

### Verify

```bash
# Discover and run the project test execution script to evaluate schema validation suite passes.
# Discover and run the project type check script to ensure static type inference aligns with runtime schemas.
# Discover and run the project module build verification script across all supported module targets.
```

**Accept when:**
- All schema validation test fixtures execute without parsing errors under both ECMAScript and CommonJS module formats.
- Static type checking completes with zero diagnostic errors across all schema definitions and inferred types.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>