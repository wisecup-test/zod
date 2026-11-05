---
version: 2
name: cross-cutting-developers-derive-runtime-input-validati-9056
description: "drizzle-zod Integration for pgTable Schema Modeling: Developers Derive Runtime Input Validation Schemas"
metadata:
  actual:
    adr_id: 90568196-393d-4a6a-8478-97408639e933
    status: accepted
    candidate_group_id: 2f9f1893-cb79-4eb9-88e7-12dd3a2d6d54
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/integration/fixtures/drizzle-zod/**
---

# drizzle-zod Integration for pgTable Schema Modeling: Developers Derive Runtime Input Validation Schemas

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DRIZZLE-001** SHOULD: Derive runtime input validation schemas directly from pgTable definitions rather than manually declaring separate zod structures.
- **R-DRIZZLE-002** MANDATORY: Execute lock-version grounding (find manifest, identify build tool, inspect lock/resolution artifact, look up exact-version docs, confirm API existence) before writing code using a versioned library.
- **R-DRIZZLE-003** MANDATORY: Apply schema transformation (pick/omit) utilities when external contract shapes must diverge from underlying table columns to avoid leaking internal database structures.

### Verify

```bash
# Discover and run the project type checking script
# (Command discovered dynamically from repository package manager/manifest)
npx tsc --noEmit

# Discover and run the project test suite
# (Command discovered dynamically from repository package manager/manifest)
npx test
```

**Accept when:**
- Type validation confirms that relational table definitions and derived validation schemas compile without diagnostic errors.
- Project integration test suites exercising schema modeling and input validation pass without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests introducing inconsistent table definitions and validation schemas are blocked until reconciled.
</enforcement>