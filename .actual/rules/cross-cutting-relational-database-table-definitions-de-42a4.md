---
version: 2
name: cross-cutting-relational-database-table-definitions-de-42a4
description: "drizzle-orm/pg-core Table Schema Modeling: Relational Database Table Definitions Declared Pgtable"
metadata:
  actual:
    adr_id: 42a44c78-f794-4163-a217-19fcf9f7db6a
    status: accepted
    candidate_group_id: 83ca0e30-9cc5-43b2-92ba-0fef3a5f1a00
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Table Schema Modeling: Relational Database Table Definitions Declared Pgtable

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for relational database schema modeling and table definitions across data access modules.

### Rules

- **R-TBL-001** MUST: Relational database table definitions MUST be declared using pgTable definitions from drizzle-orm/pg-core with typed column primitives and explicit primary key constraints.

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