---
version: 2
name: cross-cutting-developers-inspect-repository-lock-artif-acc8
description: "drizzle-zod Integration for pgTable Schema Modeling: Developers Inspect Repository Lock Artifact Determine"
metadata:
  actual:
    adr_id: acc86c38-6b60-4bf6-8ec9-281f1ef01cad
    status: accepted
    candidate_group_id: 2f9f1893-cb79-4eb9-88e7-12dd3a2d6d54
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/integration/fixtures/drizzle-zod/**
---

# drizzle-zod Integration for pgTable Schema Modeling: Developers Inspect Repository Lock Artifact Determine

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DZ-001** MUST: Developers MUST inspect the repository lock artifact to determine the exact resolved versions of drizzle-zod and drizzle-orm/pg-core before implementing or modifying schema definitions.
- **R-DZ-002** MUST: Declare relational table schemas with pgTable and derive corresponding runtime validation schemas through drizzle-zod.
- **R-DZ-003** SHOULD: Apply schema transformation utilities when external contract shapes must diverge from underlying table columns.

### Verify

```bash
# Discover and run the project type checking script
# Discover and run the project test suite
```

**Accept when:**
- Type validation confirms that relational table definitions and derived validation schemas compile without diagnostic errors.
- Project integration test suites exercising schema modeling and input validation pass without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by continuous integration static type checks and automated test execution across schema modeling test suites.
</enforcement>