# Zod Core Subsystem Modularization: Encapsulating ZodError and Parsing Helper Utilities: Engineers Discover Ecosystem Lock Artifact Within

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Core schema validation libraries require robust separation between type schema definitions, parsing execution routines, and error compilation.
- Monolithic validation architectures tend to couple error message string formatting and localization directly into schema type validators, impeding customization and increasing core bundle overhead.
- Static inspection demonstrates modular decomposition across the validation framework where error handling centers on ZodError and specialized helper modules decouple parsing operations from schema representations.

## Problem Statement

Directly coupling schema evaluation, localized issue formatting, and error throwing inside schema type declarations creates tight architectural coupling, prevents unified error handling across heterogeneous validation checks, and restricts client applications from intercepting safe validation results without exception handling overhead.

## Decision

1. MUST: Engineers MUST discover the ecosystem lock artifact within the repository and verify the exact resolved version of all validation library dependencies prior to introducing or modifying core module abstractions.

## Policy Block

- MUST Engineers MUST discover the ecosystem lock artifact within the repository and verify the exact resolved version of all validation library dependencies prior to introducing or modifying core module abstractions.

In scope:
- Core validation library modules responsible for defining schema types, parsing pipelines, and error handling structures.
- Internal helper subsystems providing parsing coordination, enumeration extraction, and localized error formatting.

Out of scope:
- External consumer application business logic consuming public validation schemas without modifying core library modules.
- Third-party validation adapters operating outside the primary validation library package boundary.

## Rationale

- Evidence demonstrates dedicated module boundaries for ZodError and helper utilities, ensuring error compilation remains completely decoupled from schema definitions.
- Providing dual parsing pathways through parse and safeParse establishes predictable runtime exception guarantees for callers requiring non-throwing validation results.
- Isolating localization and helper utilities into distinct modules enables maintainable extension of validation checks and localized messaging without altering core type evaluators.

## Consequences

Positive:
- Centralized error formatting and localized issue generation through ZodError and dedicated helper utilities.
- Consistent client ergonomics allowing callers to choose between exception-throwing parsing and safe result objects.
- Clear architectural boundaries between internal parsing helpers and public schema type contracts.

Negative:
- Increased internal module count and cross-module call depth between schema types and error helper utilities.
- Internal contract coordination overhead when updating error issue structures across helper modules.

## Alternatives

- Monolithic schema validation classes embedding error message formatting and direct exception throwing within each type validator (rejected)
  Rejected because: Couples localization and error construction to individual schema types, duplicating error formatting logic and preventing consistent non-throwing safeParse workflows
  When valid: Single-purpose lightweight validation scripts where extensible error reporting and localization are unnecessary
- Dynamic pluggable error handler registration across global validation runtime contexts (rejected)
  Rejected because: Introduces global mutable state and indirection that complicates static analysis, modular encapsulation, and deterministic error typing
  When valid: Frameworks requiring dynamic runtime provider injection across distributed multi-tenant environments

## Risks

- Tight coupling between internal parsing helper interfaces and schema definition implementations could cause breaking changes during internal module refactoring.
  Mitigation: Establish strict internal interface contracts and automated regression test suites covering parse and safeParse behavior.
  Owner: Core Validation Library Maintainers
- Performance overhead from allocating structured error contexts and intermediate validation issue arrays during high-throughput parsing.
  Mitigation: Defer detailed error message materialization until error serialization or inspection is explicitly requested on the ZodError instance.
  Owner: Core Validation Library Maintainers

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Ensure all schema type implementations define both throwing and non-throwing parsing methods adhering to the standardized error encapsulation contract.
- Maintain strict separation between locale message resolution and schema check evaluators by directing issue generation through centralized error utility modules.

## Continuation Context


Verify commands:
- Discover and execute the repository type-checking script to confirm interface compliance across core schema types and helper modules.
- Discover and run the project test execution suite targeting validation parsing and error formatting behaviors.

Accept when:
- All core schema types successfully implement parse and safeParse interfaces with zero type-checking diagnostics.
- Test execution suite verifies that validation failures produce correctly formatted ZodError instances without uncaught internal exceptions.

## Enforcement

- Verified by: Automated continuous integration pipelines executing type validation and unit test suites across core modules.
- Verified by: Peer code review auditing new schema types and helper modules against architectural encapsulation rules.
- Violation handling: Pull requests bypassing ZodError encapsulation or directly embedding error formatting in schema types will be blocked until compliant.
- Violation handling: Deprecate and refactor non-compliant direct error generation patterns in legacy module boundaries.
- Exception process: Formal architectural review submission documented in repository issue tracking requiring approval from core library maintainers.