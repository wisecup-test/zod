# Adopt Schema-Based Validation as Primary Data Storage Gateway: Data Written Primary

Status: proposed
Date: 2025-01-20
Deciders: Detection Pipeline (automated)

## Activation

This ADR is ACTIVE for all data storage operations requiring validation, serialization, or schema enforcement at the application boundary layer.

## Context

- The codebase utilizes Zod v4 schema validation extensively across test suites and core schema definitions, indicating a systematic approach to data validation at storage boundaries
- Pattern detected across 4 files with 91.55% confidence, including core schema definitions (schemas.ts) and multiple test files (description.test.ts, default.test.ts, from-json-schema.test.ts)
- The facet 'data.cache_layer' suggests this pattern serves as an intermediary validation layer between application logic and persistent storage
- Schema-based validation provides type safety, runtime validation, and serialization capabilities that bridge TypeScript compile-time types with runtime data integrity
- The pattern signature e3073fa992148e0096f809a3e9437b82 represents a consistent architectural approach to data modeling and access control

## Problem Statement

Applications require a robust mechanism to ensure data integrity at the boundary between application logic and persistent storage. Without schema-based validation, data corruption, type mismatches, and serialization errors can propagate into datastores, leading to inconsistent state, difficult debugging, and potential data loss. The system needs a declarative, type-safe approach to validate, transform, and serialize data before it reaches primary datastores.

## Decision

1. MUST: All data written to primary datastores MUST pass through schema validation using Zod v4 or equivalent schema validation library

## Policy Block

- MUST All data written to primary datastores MUST pass through schema validation using Zod v4 or equivalent schema validation library

In scope:
- All write operations to primary datastores (databases, key-value stores, document stores)
- Data serialization and deserialization at storage boundaries
- API request/response payloads that will be persisted
- Configuration data loaded from external sources before storage
- Cache layer operations where data integrity is critical

Out of scope:
- Ephemeral in-memory data structures that never persist
- Internal function parameters within a single module boundary
- Logging and debugging output
- Read-only queries that do not modify datastore state
- Performance-critical hot paths where validation overhead is prohibitive (requires explicit exception approval)

Exceptions:
- EXC-001: Performance profiling demonstrates validation overhead exceeds 10% of operation latency in critical paths
- EXC-002: Legacy system integration where schema cannot be reliably determined or enforced

## Rationale

- Pattern detected with 91.55% confidence across 4 files demonstrates consistent adoption of schema-based validation as an architectural standard
- Zod v4 provides TypeScript-first schema validation with excellent type inference, reducing duplication between runtime validation and compile-time types
- Schema validation at the datastore boundary prevents invalid data from corrupting persistent state, reducing debugging complexity and data migration costs
- The presence of comprehensive test suites (description.test.ts, default.test.ts, from-json-schema.test.ts) indicates mature testing practices around schema definitions
- Cache layer facet suggests this pattern serves as a critical intermediary ensuring data quality before expensive storage operations

## Consequences

Positive:
- Strong type safety with automatic TypeScript type inference from schema definitions, eliminating type/validation duplication
- Runtime validation catches data integrity issues before they reach persistent storage, preventing data corruption
- Declarative schema definitions serve as living documentation of data models and constraints
- Schema-based approach enables automatic generation of API documentation, JSON schemas, and validation error messages
- Centralized validation logic reduces scattered validation code throughout the application

Negative:
- Additional runtime overhead for validation on every write operation (typically 1-5ms per validation)
- Learning curve for developers unfamiliar with schema validation libraries like Zod
- Schema definitions require maintenance and versioning alongside data model evolution
- Complex nested schemas can become verbose and difficult to compose without proper abstraction
- Potential performance bottleneck in high-throughput write scenarios requiring careful optimization

## Alternatives

- TypeScript interfaces only with no runtime validation (rejected)
  Rejected because: TypeScript types are erased at runtime, providing no protection against invalid data from external sources, user input, or API responses. This approach fails to prevent data corruption in persistent storage.
  When valid: Only acceptable for purely internal, compile-time-only data structures that never cross module boundaries or persist
- Database-level constraints and validation only (rejected)
  Rejected because: Database constraints provide last-resort validation but offer poor error messages, no TypeScript integration, and require round-trip to database to detect validation failures. This increases latency and debugging difficulty.
  When valid: Should be used as a complementary defense-in-depth layer alongside application-level schema validation
- Manual validation functions scattered throughout codebase (rejected)
  Rejected because: Manual validation leads to inconsistent validation logic, duplication, maintenance burden, and increased likelihood of validation gaps. No automatic type inference or documentation generation.
  When valid: Acceptable only for one-off custom validation logic that cannot be expressed declaratively in schemas

## Risks

- Performance degradation in high-throughput write scenarios due to validation overhead
  Mitigation: Profile validation performance in critical paths, implement caching for repeated validations of identical schemas, consider async validation for non-critical writes, and use policy exception process for documented performance-critical paths
  Owner: Engineering team with performance monitoring
- Schema evolution and versioning challenges as data models change over time
  Mitigation: Implement schema versioning strategy, use backward-compatible schema changes where possible, maintain migration scripts for breaking changes, and document schema evolution in ADRs
  Owner: Architecture team and data modeling working group
- Developer bypass of validation in time-pressured situations leading to validation gaps
  Mitigation: Enforce validation through CI/CD checks, code review requirements, automated detection of unvalidated datastore writes, and clear documentation of exception process
  Owner: Engineering team and code review process

## Implementation Notes

- Start by defining schemas in a centralized schemas/ directory or co-located with data access modules, following the pattern observed in packages/zod/src/v4/core/schemas.ts
- Create comprehensive test suites for each schema covering valid inputs, invalid inputs, edge cases, default values, and transformations (following patterns in description.test.ts, default.test.ts)
- Integrate schema validation into data access layer (repositories, DAOs, or ORM models) so all writes automatically pass through validation
- Use Zod's .parse() for synchronous validation that throws on failure, or .safeParse() for validation that returns Result types for error handling
- Export TypeScript types from schemas using 'type MyType = z.infer<typeof mySchema>' to maintain single source of truth
- Consider implementing a validation middleware or decorator pattern for consistent error handling and logging across all datastore operations

## Continuation Context


Verify commands:
- grep -r '\.parse\|safeParse' packages/zod/src --include='*.ts' | wc -l
- find . -name 'schemas.ts' -o -name '*.schema.ts' | xargs grep -l 'z\.' | wc -l
- npm test -- --testPathPattern='schema|validation' --passWithNoTests

Accept when:
- All datastore write operations include schema validation calls (.parse or .safeParse) before persistence
- Schema definition files exist and are tested with dedicated test suites achieving >80% coverage
- CI pipeline includes schema validation tests that must pass before merge
- Code review checklist includes verification of schema validation for new datastore operations

## Enforcement

- Verified by: Automated CI/CD pipeline checks for presence of schema validation in datastore operations
- Verified by: Code review process with explicit checklist item for schema validation verification
- Verified by: Static analysis tools or custom linters detecting unvalidated datastore writes
- Verified by: Regular architecture audits reviewing datastore access patterns
- Violation handling: CI pipeline fails if new datastore operations lack schema validation
- Violation handling: Code review blocks merge until schema validation is added or exception is approved
- Violation handling: Runtime monitoring alerts on validation failures to detect gaps in validation coverage
- Violation handling: Quarterly architecture reviews identify and remediate validation gaps
- Exception process: Developer submits exception request with performance metrics or technical justification
- Exception process: Tech lead and architecture review board evaluate risk and approve/reject within 2 business days
- Exception process: Approved exceptions documented in code comments with ADR reference and expiration date
- Exception process: Exception registry maintained with quarterly review for removal or renewal