---
version: 2
name: cross-cutting-developers-not-alter-database-table-f4c4
description: "drizzle-zod Integration for pgTable Schema Modeling: Developers Not Alter Database Table Column"
metadata:
  actual:
    adr_id: f4c4aee0-c2d6-4fe5-82ee-5108bd70f224
    status: accepted
    candidate_group_id: 2f9f1893-cb79-4eb9-88e7-12dd3a2d6d54
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/integration/fixtures/drizzle-zod/**
---

# drizzle-zod Integration for pgTable Schema Modeling: Developers Not Alter Database Table Column

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for relational database table definitions that derive runtime validation schemas using drizzle-zod.

### Rules

- **R-DRIZZLE-001** MUST_NOT: Developers MUST NOT alter database table column definitions in pgTable declarations without reconciling the corresponding derived drizzle-zod schemas and validation boundaries.

### Verify

```bash
# Discover and run the project type checking script
# Discover and run the project test suite
```

**Accept when:**
- Type validation confirms that relational table definitions and derived validation schemas compile without diagnostic errors.
- Project integration test suites exercising schema modeling and input validation pass without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>