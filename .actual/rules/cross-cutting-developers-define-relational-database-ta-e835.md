---
version: 2
name: cross-cutting-developers-define-relational-database-ta-e835
description: "drizzle-zod Integration for pgTable Schema Modeling: Developers Define Relational Database Table Schemas"
metadata:
  actual:
    adr_id: e835139c-e51b-4835-ba8d-eed9222c8403
    status: accepted
    candidate_group_id: 2f9f1893-cb79-4eb9-88e7-12dd3a2d6d54
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/integration/fixtures/drizzle-zod/**
---

# drizzle-zod Integration for pgTable Schema Modeling: Developers Define Relational Database Table Schemas

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for relational database table definitions that derive runtime validation schemas using drizzle-zod.

### Rules

- **R-DZ-001** MUST: Developers MUST define relational database table schemas using pgTable from drizzle-orm/pg-core when adopting schema derivation through drizzle-zod.
- **R-DZ-002** MANDATORY: Execute lock-version grounding before writing code that uses a versioned library (discover dependency manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for exact version, confirm APIs exist, re-run per dependency at point of use).
- **R-DZ-003** MANDATORY: Declare relational table schemas with pgTable and derive corresponding runtime validation schemas through drizzle-zod.
- **R-DZ-004** MANDATORY: Apply schema transformation utilities (omitting and picking) when external contract shapes must diverge from underlying table columns.

### Verify

```bash
# Discover and run the project type checking script to verify derived drizzle-zod validation schemas align with pgTable declarations
# Discover and run the project test suite to verify that integration tests for schema models pass
```

**Accept when:**
- Type validation confirms that relational table definitions and derived validation schemas compile without diagnostic errors.
- Project integration test suites exercising schema modeling and input validation pass without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration static type checks and automated test execution across schema modeling test suites verify compliance.
</enforcement>