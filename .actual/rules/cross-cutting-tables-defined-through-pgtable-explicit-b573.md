---
version: 2
name: cross-cutting-tables-defined-through-pgtable-explicit-b573
description: "drizzle-orm/pg-core Relational Schema Definition: Tables Defined Through Pgtable Explicit Column"
metadata:
  actual:
    adr_id: b5737d9e-caf3-4481-b187-ddcbf25aaf1d
    status: accepted
    candidate_group_id: 58ee9597-84ce-4c31-ada1-72707dd220c2
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/integration/fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Relational Schema Definition: Tables Defined Through Pgtable Explicit Column

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for relational database schema definitions and data model declarations.

### Rules

- **R-PG-001** MUST: Tables MUST be defined through pgTable with explicit column type declarations and primary key constraints.
- **R-PG-002** MANDATORY: Execute the discovery policy and lock-version grounding sequence before writing code that uses a versioned library.
- **R-PG-003** MANDATORY: Define database tables in designated schema modules using pgTable, declaring explicit primary keys and column modifiers.

### Verify

```bash
# Discover and execute the repository type-checking script to ensure schema definitions satisfy compile-time constraints.
# Discover and run the project test suite to verify schema instantiation and data model operations.
```

**Accept when:**
- The project type-checking script passes with zero diagnostic errors across schema definitions.
- All database model verification suites execute successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline type verification and pull request peer code review.
</enforcement>