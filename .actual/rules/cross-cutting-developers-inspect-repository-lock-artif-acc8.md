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

These rules are ALWAYS ACTIVE for:
- Relational database table definitions that derive runtime validation schemas using drizzle-zod.

### Rules

- **R-DM-001** MUST: Developers MUST inspect the repository lock artifact to determine the exact resolved versions of drizzle-zod and drizzle-orm/pg-core before implementing or modifying schema definitions.

### Verify

- Discover and run the project type checking script to verify that derived drizzle-zod validation schemas align with pgTable declarations.
- Discover and run the project test suite to verify that integration tests for schema models pass.

**Accept when:**

- Type validation confirms that relational table definitions and derived validation schemas compile without diagnostic errors.
- Project integration test suites exercising schema modeling and input validation pass without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Continuous integration static type checks.
- Verified by: Automated test execution across schema modeling test suites.
- Violation handling: Pull requests introducing inconsistent table definitions and validation schemas are blocked until reconciled.
- Exception process: Submit an architectural exception request documenting domain requirements that necessitate decoupled validation schemas.
</enforcement>
