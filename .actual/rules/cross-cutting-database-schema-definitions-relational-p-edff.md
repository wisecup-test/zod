---
version: 2
name: cross-cutting-database-schema-definitions-relational-p-edff
description: "drizzle-orm/pg-core Relational Schema Definition: Database Schema Definitions Relational Persistence Utilize"
metadata:
  actual:
    adr_id: edff3b07-ca44-4819-901c-c79f92cabd75
    status: accepted
    candidate_group_id: 58ee9597-84ce-4c31-ada1-72707dd220c2
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/integration/fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Relational Schema Definition: Database Schema Definitions Relational Persistence Utilize

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DB-001** MUST: Database schema definitions for relational persistence MUST utilize drizzle-orm/pg-core constructs to declare table structures.

### Verify

```bash
# Discover and execute the repository type-checking script to ensure schema definitions satisfy compile-time constraints.
# Discover and run the project test suite to verify schema instantiation and data model operations.
```

**Accept when:**
- The project type-checking script passes with zero diagnostic errors across schema definitions.
- All database model verification suites execute successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline type verification and pull request peer code review enforce compliance.
</enforcement>