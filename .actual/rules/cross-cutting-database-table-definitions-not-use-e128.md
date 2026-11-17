---
version: 2
name: cross-cutting-database-table-definitions-not-use-e128
description: "drizzle-orm/pg-core Table Schema Modeling: Database Table Definitions Not Use Untyped"
metadata:
  actual:
    adr_id: e128d00d-299d-4db5-805a-93b1ff39c3df
    status: accepted
    candidate_group_id: 83ca0e30-9cc5-43b2-92ba-0fef3a5f1a00
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Table Schema Modeling: Database Table Definitions Not Use Untyped

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for relational database schema modeling and table definitions across data access modules.

### Rules

- **R-DB-001** MUST_NOT: Database table definitions MUST NOT use untyped raw string mappings or bypass primary key designations.

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