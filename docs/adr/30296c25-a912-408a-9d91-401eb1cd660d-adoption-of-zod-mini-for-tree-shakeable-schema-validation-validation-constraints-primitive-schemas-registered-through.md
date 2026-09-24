# Adoption of zod/mini for Tree-Shakeable Schema Validation: Validation Constraints Primitive Schemas Registered Through

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Application packages require structured input validation and runtime type assertion across boundary interfaces.
- Monolithic validation libraries introduce substantial bundle overhead when imported indiscriminately across distributed packages.
- The codebase establishes schema definitions utilizing modular imports and functional check composition to support tree-shaking and execution efficiency.
- Benchmark and treeshaking test fixtures demonstrate repeated usage of the mini entry point for schema parsing and string validation checks.

## Problem Statement

Standard monolithic schema validation libraries bundle comprehensive feature suites that increase artifact size and introduce parsing overhead in performance-critical modules. A lightweight, tree-shakeable schema definition mechanism is required to enforce strict input validation contracts while minimizing runtime memory and execution footprints.

## Decision

1. MUST: Validation constraints on primitive schemas MUST be registered through the check method utilizing functional constraint functions.

## Policy Block

- MUST Validation constraints on primitive schemas MUST be registered through the check method utilizing functional constraint functions.

In scope:
- All workspace packages declaring schema definitions for input validation, payload verification, and runtime contract assertions.
- Performance-sensitive and bundle-constrained modules requiring modular validation pipelines.

Out of scope:
- Modules with zero runtime schema validation or deserialization requirements.
- Legacy subsystem boundaries that do not perform dynamic input assertion.

Exceptions:
- EXC-20-001: A third-party module interface requires an incompatible schema validation interface.

## Rationale

- Evidence from multiple packages confirms the consistent selection of zod/mini for schema definition and parsing.
- Modular check chains decouple validation logic into discrete functions, permitting tree-shakers to discard unused validator code.
- Benchmarking and bundle analysis demonstrate superior throughput and minimal artifact footprint compared to monolithic alternatives.

## Consequences

Positive:
- Eliminates unused validator code from production bundles through granular subpath exports.
- Standardizes schema definitions around functional, composable check pipelines.
- Improves parsing throughput across performance-critical runtime data paths.

Negative:
- Requires developers to adopt functional constraint composition rather than traditional fluent chaining methods.
- Requires disciplined discovery of module subpath exports and API signatures from repository lock artifacts.

## Alternatives

- Monolithic default library export (rejected)
  Rejected because: Bundles all schema types and validator functions regardless of usage, inflating deployment artifacts and degrading tree-shaking efficacy.
  When valid: Valid only in non-bundled server environments where package size has no operational impact.
- Handcrafted manual type guard functions (rejected)
  Rejected because: Lacks automated schema composition, centralized error reporting, and parsing safety guarantees.
  When valid: Valid only for trivial single-property checks with zero external dependency tolerance.

## Risks

- Developers might inadvertently import monolithic exports instead of the mini subpath, causing bundle size regression.
  Mitigation: Configure automated lint rules and import boundary constraints to restrict import paths to the approved mini entry point.
  Owner: Engineering Team
- API discrepancies between monolithic and mini functional constraint methods could cause implementation confusion.
  Mitigation: Document functional constraint patterns and mandate lock artifact documentation review prior to schema authoring.
  Owner: Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- When constructing complex object schemas, import object and individual validator functions directly from the mini subpath rather than importing full monolithic suites.
- Encapsulate schema validation checks inside dedicated validation boundaries before passing validated domain payloads to internal business logic.

## Continuation Context


Verify commands:
- # Discover the project test runner from the workspace manifest and execute test verification
- # Discover the project build script to verify bundle treeshaking and schema resolution
- # Inspect the repository lock artifact to confirm the exact resolved dependency version

Accept when:
- All schema definitions import runtime validation utilities from zod/mini and pass workspace verification.
- Functional constraint pipelines using check, minLength, maxLength, and related validators execute without runtime evaluation errors.
- Input data validation parsing resolves successfully on valid inputs and rejects invalid payloads with appropriate error structures.

## Enforcement

- Verified by: Automated static analysis and linting checks in continuous integration pipelines.
- Verified by: Code review verification of module import declarations and schema composition patterns.
- Violation handling: Continuous integration static analysis checks fail on non-compliant import paths.
- Violation handling: Pull requests containing disallowed monolithic imports or unvalidated input parsing are blocked until corrected.
- Exception process: Submit an architectural review request detailing technical constraints preventing adoption of the mini module entry point.