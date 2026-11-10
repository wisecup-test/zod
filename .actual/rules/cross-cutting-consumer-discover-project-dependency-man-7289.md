---
version: 2
name: cross-cutting-consumer-discover-project-dependency-man-7289
description: "drizzle-orm/pg-core Table Schema Modeling: Consumer Discover Project Dependency Manifest Lock"
metadata:
  actual:
    adr_id: 7289ee93-5386-488f-a0cb-14f0dc7fc8b1
    status: accepted
    candidate_group_id: 83ca0e30-9cc5-43b2-92ba-0fef3a5f1a00
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Table Schema Modeling: Consumer Discover Project Dependency Manifest Lock

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DBC-001** MUST: The consumer MUST discover the project dependency manifest and lock artifact to resolve and verify the exact installed version of the table modeling library before declaring schema definitions.

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