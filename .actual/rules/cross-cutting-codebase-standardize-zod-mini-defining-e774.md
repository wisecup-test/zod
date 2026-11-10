---
version: 2
name: cross-cutting-codebase-standardize-zod-mini-defining-e774
description: "Adoption of @zod/mini for Modular Schema Validation: Codebase Standardize Zod Mini Defining Lightweight"
metadata:
  actual:
    adr_id: e774e3b6-7b96-4f54-a51f-9fcc97de9743
    status: accepted
    candidate_group_id: 19ba1074-3608-4fc6-9490-5ff43e413b98
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/internal-types/**
---

# Adoption of @zod/mini for Modular Schema Validation: Codebase Standardize Zod Mini Defining Lightweight

Scope: applies to `packages/integration/fixtures/internal-types/**`.

These rules are ALWAYS ACTIVE for modules defining runtime schema validation contracts, data transfer object validation, or type integrity boundaries.

### Rules

- **R-ZOD-001** MUST: The codebase MUST standardize on @zod/mini for defining lightweight runtime schema validation contracts and structured data parsing.

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