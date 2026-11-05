---
version: 2
name: cross-cutting-custom-enumerations-structured-array-col-8b66
description: "drizzle-orm/pg-core Relational Schema Definition: Custom Enumerations Structured Array Columns Declared"
metadata:
  actual:
    adr_id: 8b66d836-2558-48c2-8910-5943ba42fe29
    status: accepted
    candidate_group_id: 58ee9597-84ce-4c31-ada1-72707dd220c2
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/integration/fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Relational Schema Definition: Custom Enumerations Structured Array Columns Declared

Scope: applies to `packages/integration/fixtures/drizzle-zod/**`.

These rules are ALWAYS ACTIVE for relational database schema definitions and data model declarations.

### Rules

- **R-PG-001** SHOULD: Custom enumerations and structured array columns SHOULD be declared using pg-core enum and array builder functions.
- **R-PG-002** MANDATORY: The consumer MUST derive build tools, file names, commands, package managers, and version numbers from the project repository.
- **R-PG-003** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect lock/resolution artifact for exact version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run at point of use for version-sensitive behavior.
- **R-PG-004** MANDATORY: Define database tables in designated schema modules using pgTable, declaring explicit primary keys and column modifiers.
- **R-PG-005** MANDATORY: Derive validation or data transfer schemas from defined database tables using companion schema utilities where required.

### Verify

```bash
# Discover and execute the repository type-checking script to ensure schema definitions satisfy compile-time constraints.
# Discover and run the project test suite to verify schema instantiation and data model operations.
```

**Accept when:**
- The project type-checking script passes with zero diagnostic errors across schema definitions.
- All database model verification suites execute successfully.

<enforcement>
Verification is mandatory. Claude Code MUST NOT skip or defer verification. Pull requests introducing non-standard relational schema definitions will be blocked until brought into compliance.
</enforcement>