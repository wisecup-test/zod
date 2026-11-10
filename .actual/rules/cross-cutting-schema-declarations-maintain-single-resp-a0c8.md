---
version: 2
name: cross-cutting-schema-declarations-maintain-single-resp-a0c8
description: "drizzle-orm/pg-core Table Schema Modeling: Schema Declarations Maintain Single Responsibility Separation"
metadata:
  actual:
    adr_id: a0c87a46-3721-47bd-b100-0ccc4412ad30
    status: accepted
    candidate_group_id: 83ca0e30-9cc5-43b2-92ba-0fef3a5f1a00
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Table Schema Modeling: Schema Declarations Maintain Single Responsibility Separation

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-SCHEMA-001** SHOULD: Schema declarations SHOULD maintain single-responsibility separation between table definitions and input validation schema generators.

### Verify

```bash
command -v discover_build_tool >/dev/null 2>&1 && discover_and_run_schema_typecheck || echo 'Run project typecheck command'
command -v discover_test_runner >/dev/null 2>&1 && discover_and_run_schema_unit_tests || echo 'Run project test suite'
```

**Accept when:**
- All database table schema declarations pass static type verification without unresolved column constraints or type errors.
- Relational models correctly instantiate serial primary keys and typed enum array column structures.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>