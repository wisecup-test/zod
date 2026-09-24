# Zod Schema Validation Adoption: Modules Not Bypass Schema Validation Coercing

Status: proposed
Date: 2025-05-15
Deciders: Detection Pipeline (automated)

## Context

- External inputs and structured payloads require runtime verification to ensure adherence to expected data shapes.
- Static type checking does not guarantee data structure integrity during execution when untrusted or dynamic inputs are processed.
- The project incorporates zod across multiple modules to construct declarative schemas and validate input objects at execution boundaries.

## Problem Statement

Without runtime schema validation, unvalidated payloads can introduce runtime exceptions and data corruption across system boundaries. The system requires a declarative, type-safe schema library to enforce structural invariants on input data.

## Decision

1. MUST_NOT: Modules MUST_NOT bypass schema validation by coercing unverified payloads directly into expected types.

## Policy Block

- MUST_NOT Modules MUST_NOT bypass schema validation by coercing unverified payloads directly into expected types.

In scope:
- Modules defining, validating, or evaluating structured data payloads across execution boundaries.
- Components processing external or unverified input structures.

Out of scope:
- Internal private functions operating on previously validated and strictly encapsulated types.
- Performance-critical inner loops where inputs have been pre-validated and verified immutable.

## Rationale

- Adopting zod provides composable schema declarations and consistent runtime validation logic.
- Static evidence across multiple modules shows consistent reliance on z.object definitions and schema parse invocations.
- Enforcing runtime validation prevents malformed payloads from propagating into downstream operations.

## Consequences

Positive:
- Guarantees runtime payload integrity and structural conformity across system boundaries.
- Provides unified schema definitions that connect runtime validation with static type inference.
- Prevents data corruption and unexpected execution errors caused by malformed input structures.

Negative:
- Introduces runtime computational overhead for schema parsing and validation of complex objects.
- Adds an external dependency that must be maintained and tracked across repository modules.

## Alternatives

- Manual conditional validation checks (rejected)
  Rejected because: Manual validation checks are error-prone, verbose, and difficult to keep synchronized with evolving data models.
  When valid: Valid in isolated single-function utilities with zero external dependencies and trivial primitive validation needs.
- Compile-time type assertions without runtime validation (rejected)
  Rejected because: Type assertions bypass execution-time validation, allowing malformed external payloads to cause downstream runtime failures.
  When valid: Valid strictly within internal execution contexts where data structures have already been validated at the perimeter.

## Risks

- Performance degradation when parsing large data volumes or deeply nested schemas in hot execution paths.
  Mitigation: Profile validation overhead in latency-sensitive paths and validate data once at the ingestion perimeter.
  Owner: engineering team
- Schema drift between boundary schemas and internal data representations.
  Mitigation: Derive static types directly from zod schemas using type inference utilities.
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
- Declare reusable schemas for domain models using z.object and composite schema primitives.
- Invoke the parse method at boundary entry points to fail fast on invalid input structures before proceeding with domain logic.

## Continuation Context


Verify commands:
- # Discover the project verification script from the repository manifest and execute validation
- # Discover the project type check configuration and execute static analysis

Accept when:
- All data structures entering validation boundaries conform to defined zod schemas and pass schema parse calls without error.
- Repository verification scripts execute successfully with zero validation or type checking errors.

## Enforcement

- Verified by: Automated continuous integration test suites and static analysis checks.
- Verified by: Peer code reviews verifying that untrusted inputs pass through schema parse methods.
- Violation handling: Pull requests introducing unvalidated runtime boundary inputs will be blocked from merging until schema validation is added.
- Exception process: Exceptions for performance-critical inner loops require profiling evidence submitted to the engineering team for architectural review.