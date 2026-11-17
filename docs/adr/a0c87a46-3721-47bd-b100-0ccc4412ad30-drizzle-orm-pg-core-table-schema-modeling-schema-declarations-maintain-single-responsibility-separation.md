---
version: 2
name: a0c87a46-3721-47bd-b100-0ccc4412ad30-drizzle-orm-pg-core-table-schema-modeling-schema-declarations-maintain-single-responsibility-separation
description: "drizzle-orm/pg-core Table Schema Modeling: Schema Declarations Maintain Single Responsibility Separation"
metadata:
  actual:
    adr_id: a0c87a46-3721-47bd-b100-0ccc4412ad30
    status: accepted
    candidate_group_id: 83ca0e30-9cc5-43b2-92ba-0fef3a5f1a00
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Table Schema Modeling: Schema Declarations Maintain Single Responsibility Separation

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/integration`

Applies to:
- `fixtures/drizzle-zod/**`

## Context

- The codebase includes schema definitions that model database tables programmatically through typed schema definition libraries.
- Table definitions combine schema definition APIs from drizzle-orm/pg-core with typed serial primary keys and enum array columns.
- Static type safety for database entities is enforced at compile time through declarative schema primitives rather than ambient SQL declarations.

## Problem Statement

Database schema definitions in TypeScript projects often suffer from drift between raw relational database DDL statements and application-level domain representations. Defining database tables with manual type annotations or disparate schema systems introduces type mismatches and runtime persistence failures. The project requires a typed schema definition mechanism that captures relational constraints such as serial primary keys and enum array columns while maintaining direct integration with validation utilities.

## Decision

1. SHOULD: Schema declarations SHOULD maintain single-responsibility separation between table definitions and input validation schema generators.

## Policy Block

- SHOULD Schema declarations SHOULD maintain single-responsibility separation between table definitions and input validation schema generators.

In scope:
- Relational database schema modeling and table definitions across data access modules.

Out of scope:
- Transient in-memory structures and third-party data serialization schemas.

## Rationale

- drizzle-orm/pg-core provides composable, type-safe column helper functions that map directly to underlying relational database features such as serial primary keys and typed enum arrays.
- Declaring relational tables through programmatic schema APIs allows type inference to propagate across database queries and validation layers without separate code generation steps.
- Evidence demonstrates explicit usage of pgTable, serial, and labelEnum array constructs within integration fixture definitions.

## Consequences

Positive:
- Relational database tables gain end-to-end static type safety derived directly from schema declarations.
- Database column constraints such as serial primary keys and enum arrays are validated at compile time.
- Eliminates out-of-band schema mapping synchronization layers between application code and database persistence.

Negative:
- Persistence data modeling is tightly coupled to the column helper APIs of the adopted library dialect.
- Complex database migrations and custom dialect capabilities require adherence to library-specific abstraction primitives.

## Alternatives

- Raw SQL schema migration files with ambient type definitions (rejected)
  Rejected because: Raw SQL files lack bidirectional compile-time type inference and permit silent drift between application code and database constraints.
  When valid: Legacy applications relying exclusively on external database migration tooling without unified language typing.
- Class-based object-relational mapping models with decorator annotations (rejected)
  Rejected because: Decorator-based object-relational mapping models introduce heavy runtime reflection metadata and decouple schema declarations from functional type inference.
  When valid: Enterprise frameworks enforcing object-oriented active-record persistence patterns.

## Risks

- Breaking API changes across library versions could impact table definitions and column helper syntax.
  Mitigation: Enforce strict dependency lockfile grounding and verify documentation against the exact resolved package version before modifying schemas.
  Owner: engineering team
- Single-file fixture evidence indicates the pattern may not be uniformly adopted across all production persistence layers.
  Mitigation: Audit all data access packages during code reviews to evaluate whether schema definitions should be standardized repository-wide.
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
- Inspect the project repository to identify existing schema definition patterns, database configuration artifacts, and shared client bindings.
- Verify that database column data types and constraint helper functions match target persistence engine specifications.

## Continuation Context


Verify commands:
- command -v discover_build_tool >/dev/null 2>&1 && discover_and_run_schema_typecheck || echo 'Run project typecheck command'
- command -v discover_test_runner >/dev/null 2>&1 && discover_and_run_schema_unit_tests || echo 'Run project test suite'

Accept when:
- All database table schema declarations pass static type verification without unresolved column constraints or type errors.
- Relational models correctly instantiate serial primary keys and typed enum array column structures.

## Enforcement

- Verified by: Automated static type analysis executed during continuous integration workflows.
- Verified by: Peer review of database schema declarations and migration pull requests.
- Violation handling: Pull requests introducing untyped or non-standard persistence schema definitions must be blocked until compliant with table modeling rules.
- Violation handling: Non-compliant schema definitions must be refactored to use standard table modeling primitives.
- Exception process: Exceptions for non-standard persistence structures or raw dialect access must be submitted with architectural justification and approved by the lead persistence architect.