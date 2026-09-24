# drizzle-orm/pg-core Table Schema Definition: Database Table Schemas Not Declared Raw

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Relational schema definitions require static type guarantees and consistent programmatic definitions.
- The codebase contains a fixture defining table structures using drizzle-orm/pg-core column builder functions.
- Adoption of structured table definitions provides compile-time alignment between schema representations and application queries.

## Problem Statement

Defining relational database structures without standardized type-safe schema definitions leads to drift between persistent data models and application logic. The architecture requires a uniform approach to model tables, columns, and data types programmatically while providing static typing across the data layer.

## Decision

1. MUST_NOT: Database table schemas MUST_NOT be declared using raw SQL strings without drizzle-orm/pg-core schema definitions.

## Policy Block

- MUST_NOT Database table schemas MUST_NOT be declared using raw SQL strings without drizzle-orm/pg-core schema definitions.

In scope:
- Relational database table schemas and column definitions within the application data layer.

Out of scope:
- Non-relational data stores, ephemeral cache keys, and external third-party API payloads.

## Rationale

- Declaring database models via drizzle-orm/pg-core enforces strict column-level type safety across schema definitions.
- Programmatic schema modeling enables schema inference and downstream validation derivation without manual type duplication.
- Typed column builders ensure relational constraints and compound data structures match database engine capabilities.

## Consequences

Positive:
- Provides compile-time type safety for table columns and relational definitions.
- Enables direct integration with schema-derived validation utilities.
- Centralizes table structure definitions in programmatic schema declarations.

Negative:
- Couples data layer definitions to a specific database modeling library and dialect.
- Requires migration effort if target database engine changes.
- Adds abstraction over direct SQL data definition statements.

## Alternatives

- Raw SQL migration scripts without programmatic table definition objects (rejected)
  Rejected because: Lacks compile-time static type generation and requires maintaining duplicate TypeScript interfaces for query results.
  When valid: When utilizing database engines unsupported by modern object-relational mapping libraries or when database schemas are managed exclusively by external database administrators.
- Alternative object-relational mapping frameworks (rejected)
  Rejected because: Introduces heavier runtime overhead and deviates from lightweight schema-first definition patterns.
  When valid: When legacy persistence layers already mandate an alternative object-relational mapping framework.

## Risks

- Limited evidence in the codebase suggests schema modeling conventions may be experimental or confined to fixture environments.
  Mitigation: Verify architectural consensus across production modules prior to broader schema migrations.
  Owner: Data Architecture Team
- Dialect coupling may complicate multi-database support if non-PostgreSQL engines are required.
  Mitigation: Isolate dialect-specific column builders within dedicated database adapter modules.
  Owner: Data Architecture Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Define table structures in dedicated schema modules where column builder functions specify primary keys, types, and array attributes.
- Derive validation schemas and query result types directly from the schema definitions to maintain synchronization.

## Continuation Context


Verify commands:
- Discover the project test runner configuration and execute test suites targeting data modeling modules.
- Discover the repository type checking command and run it to verify static type conformity of schema declarations.

Accept when:
- All data modeling tests pass without failures.
- Type checking completes with zero diagnostic errors across schema definitions.

## Enforcement

- Verified by: Continuous integration type checking and automated test pipelines.
- Verified by: Peer code review for all pull requests modifying data models.
- Violation handling: Automated pipeline failures blocking merge of non-compliant schema definitions.
- Violation handling: Code review rejection requiring alignment with approved data modeling conventions.
- Exception process: Submit an architectural review request with justification for dialect exceptions or legacy schema requirements.