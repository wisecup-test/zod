---
version: 2
name: b5737d9e-caf3-4481-b187-ddcbf25aaf1d-drizzle-orm-pg-core-relational-schema-definition-tables-defined-through-pgtable-explicit-column
description: "drizzle-orm/pg-core Relational Schema Definition: Tables Defined Through Pgtable Explicit Column"
metadata:
  actual:
    adr_id: b5737d9e-caf3-4481-b187-ddcbf25aaf1d
    status: accepted
    candidate_group_id: 58ee9597-84ce-4c31-ada1-72707dd220c2
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/integration/fixtures/drizzle-zod/**
---

# drizzle-orm/pg-core Relational Schema Definition: Tables Defined Through Pgtable Explicit Column

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `packages/integration/fixtures/drizzle-zod/**`

## Context

- The project requires structured and type-safe relational database schema definitions for data persistence.
- Table definitions using drizzle-orm/pg-core constructs appear in isolated fixture code.
- Evidence of this modeling style is currently confined to a single fixture file without repository-wide adoption.

## Problem Statement

The codebase requires a standardized approach to defining relational database table schemas and associated column data types, but current evidence reflects only localized fixture usage without verified cross-package adoption.

## Decision

1. MUST: Tables MUST be defined through pgTable with explicit column type declarations and primary key constraints.

## Policy Block

- MUST Tables MUST be defined through pgTable with explicit column type declarations and primary key constraints.

In scope:
- Relational database schema definitions and data model declarations.

Out of scope:
- Non-relational data persistence, transient memory stores, and third-party external service payload definitions.

## Rationale

- Declaring schemas using drizzle-orm/pg-core ensures type-level synchronization between database tables and application domain entities.
- Declarative table builders provide compile-time safety for column types, primary keys, and enumerations.
- The evidence is restricted to a single fixture file, requiring proposal status and low adoption confidence until widespread production usage is demonstrated.

## Consequences

Positive:
- Provides type-safe schema definitions directly in application code.
- Ensures consistency across relational table declarations and column constraints.

Negative:
- Couples data access definitions to dialect-specific schema builders.
- Requires strict synchronization between database migrations and application schema declarations.

## Alternatives

- Manual SQL schema declarations (rejected)
  Rejected because: Lacks compile-time type inference and increases risk of divergence between database structures and application types.
  When valid: When operating in environments that prohibit ORM schema abstractions.
- Alternative object-relational mapping frameworks (deferred)
  Rejected because: Current evidence specifically observes drizzle-orm/pg-core constructs in fixture code.
  When valid: When enterprise requirements necessitate alternative data mapping paradigms across non-relational datastores.

## Risks

- Adopting an architectural standard based solely on fixture code may not reflect production architecture intent.
  Mitigation: Validate actual production data storage patterns across application packages before enforcing repository-wide adoption.
  Owner: engineering team
- API surface mismatches across library versions can lead to invalid schema declarations.
  Mitigation: Follow mandatory lock-version grounding before utilizing dialect-specific schema builder functions.
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
- Define database tables in designated schema modules using pgTable, declaring explicit primary keys and column modifiers.
- Derive validation or data transfer schemas from defined database tables using companion schema utilities where required.

## Continuation Context


Verify commands:
- Discover and execute the repository type-checking script to ensure schema definitions satisfy compile-time constraints.
- Discover and run the project test suite to verify schema instantiation and data model operations.

Accept when:
- The project type-checking script passes with zero diagnostic errors across schema definitions.
- All database model verification suites execute successfully.

## Enforcement

- Verified by: Automated continuous integration pipeline type verification.
- Verified by: Pull request peer code review.
- Violation handling: Pull requests introducing non-standard relational schema definitions will be blocked until brought into compliance.
- Exception process: Exceptions must be documented in an architectural exception request and approved by data architecture leads.