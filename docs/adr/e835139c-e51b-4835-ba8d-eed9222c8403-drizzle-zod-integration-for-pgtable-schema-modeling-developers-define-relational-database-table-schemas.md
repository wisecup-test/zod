---
version: 2
name: e835139c-e51b-4835-ba8d-eed9222c8403-drizzle-zod-integration-for-pgtable-schema-modeling-developers-define-relational-database-table-schemas
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

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `packages/integration/fixtures/drizzle-zod/**`

## Context

- The codebase contains relational table declarations using column builders from drizzle-orm/pg-core paired with drizzle-zod and zod validation.
- The observed pattern is isolated to a single integration test fixture module.
- Static analysis indicates high significance for the fixture pattern but does not substantiate widespread production adoption across multiple application modules.

## Problem Statement

Maintaining duplicate definitions for database persistence schemas and application input validation models creates synchronization overhead and risks schema divergence between validation contracts and storage structures.

## Decision

1. MUST: Developers MUST define relational database table schemas using pgTable from drizzle-orm/pg-core when adopting schema derivation through drizzle-zod.

## Policy Block

- MUST Developers MUST define relational database table schemas using pgTable from drizzle-orm/pg-core when adopting schema derivation through drizzle-zod.

In scope:
- Relational database table definitions that derive runtime validation schemas using drizzle-zod.

Out of scope:
- Persistence layers that do not use relational table definitions or where validation is handled by independent protocol specifications.

## Rationale

- Coupling drizzle-orm/pg-core table definitions with drizzle-zod eliminates manual schema synchronization between database columns and input validation schemas.
- The detected pgTable declaration demonstrates serial primary keys and enum array columns that require consistent runtime type enforcement.
- Observed usage is restricted to a single integration fixture file, indicating candidate exploration rather than an established cross-project standard.

## Consequences

Positive:
- Eliminates redundant schema definitions across database models and validation layers.
- Ensures database table constraints and runtime input validation contracts remain synchronized.

Negative:
- Couples application validation models directly to physical database column representations.
- Restricts data modeling conventions to column types and constructs supported by the schema derivation utility.

## Alternatives

- Independent manual declaration of validation schemas alongside relational tables (rejected)
  Rejected because: Maintaining separate schema definitions duplicates schema structure and increases the risk of divergence between database columns and validation rules.
  When valid: When application input contracts intentionally diverge significantly from persistence storage models.
- Database-only constraint validation without application-level schema generation (rejected)
  Rejected because: Fails to reject malformed input payloads prior to executing persistence queries.
  When valid: When payload validation is completely handled by an upstream gateway layer.

## Risks

- Directly deriving validation schemas from database models can inadvertently leak internal database column structures to public API boundaries.
  Mitigation: Use schema omitting and picking utilities to strip sensitive database columns before exposing derived schemas to external callers.
  Owner: engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Declare relational table schemas with pgTable and derive corresponding runtime validation schemas through drizzle-zod.
- Apply schema transformation utilities when external contract shapes must diverge from underlying table columns.

## Continuation Context


Verify commands:
- Discover and run the project type checking script to verify that derived drizzle-zod validation schemas align with pgTable declarations.
- Discover and run the project test suite to verify that integration tests for schema models pass.

Accept when:
- Type validation confirms that relational table definitions and derived validation schemas compile without diagnostic errors.
- Project integration test suites exercising schema modeling and input validation pass without failure.

## Enforcement

- Verified by: Continuous integration static type checks.
- Verified by: Automated test execution across schema modeling test suites.
- Violation handling: Pull requests introducing inconsistent table definitions and validation schemas are blocked until reconciled.
- Exception process: Submit an architectural exception request documenting domain requirements that necessitate decoupled validation schemas.