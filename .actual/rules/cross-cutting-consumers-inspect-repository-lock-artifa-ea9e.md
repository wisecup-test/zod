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

These rules are ALWAYS ACTIVE for:
- Relational database schema definitions and data model declarations.

### Rules

- **R-DM-001** MUST: Consumers MUST inspect the repository lock artifact to determine the exact resolved version of the data modeling dependency prior to applying schema declarations.

### Verify

- Discover and execute the repository type-checking script to ensure schema definitions satisfy compile-time constraints.
- Discover and run the project test suite to verify schema instantiation and data model operations.

**Accept when:**

- The project type-checking script passes with zero diagnostic errors across schema definitions.
- All database model verification suites execute successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline type verification.
- Verified by: Pull request peer code review.
- Violation handling: Pull requests introducing non-standard relational schema definitions will be blocked until brought into compliance.
- Exception process: Exceptions must be documented in an architectural exception request and approved by data architecture leads.
</enforcement>
