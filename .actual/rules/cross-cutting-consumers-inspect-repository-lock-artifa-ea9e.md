---
version: 2
name: cross-cutting-consumers-inspect-repository-lock-artifa-ea9e
description: "drizzle-orm/pg-core Relational Schema Definition: Consumers Inspect Repository Lock Artifact Determine"
metadata:
  actual:
    adr_id: ea9e4be2-d086-46bf-a0ee-06aa850e22cc
    status: accepted
    candidate_group_id: 58ee9597-84ce-4c31-ada1-72707dd220c2
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/integration/fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Relational Schema Definition: Consumers Inspect Repository Lock Artifact Determine

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DRIZZLE-001** MUST: Consumers MUST inspect the repository lock artifact to determine the exact resolved version of the data modeling dependency prior to applying schema declarations.
- **R-DRIZZLE-002** MUST: Follow mandatory lock-version grounding before utilizing dialect-specific schema builder functions.
- **R-DRIZZLE-003** MUST: Define database tables in designated schema modules using pgTable, declaring explicit primary keys and column modifiers.

### Verify

```bash
# Discover and execute the repository type-checking script to ensure schema definitions satisfy compile-time constraints.
# Discover and run the project test suite to verify schema instantiation and data model operations.
npm run typecheck
npm test
```

**Accept when:**
- The project type-checking script passes with zero diagnostic errors across schema definitions.
- All database model verification suites execute successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline type verification and pull request peer code review.
</enforcement>