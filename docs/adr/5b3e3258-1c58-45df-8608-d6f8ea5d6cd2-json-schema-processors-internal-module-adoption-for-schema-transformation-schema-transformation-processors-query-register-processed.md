# json-schema-processors Internal Module Adoption for Schema Transformation: Schema Transformation Processors Query Register Processed

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Schema generation requires mapping heterogeneous schema definitions into standardized schema representations while accommodating recursive and nested schemas.
- Monolithic transformation pipelines suffer from maintainability bottlenecks and lack clear isolation boundaries between distinct schema types.
- Context-bound state management is necessary during transformation traversal to prevent infinite recursion on cyclical data models and eliminate duplicate processing.
- Core library modularity demands separating top-level schema generation coordination from type-specific transformation processors.

## Problem Statement

Without a modular processor architecture for schema transformation, schema conversion logic becomes tightly coupled within monolithic generator routines. This lack of modular separation prevents isolated testing of individual schema conversions, complicates support for recursive schema references, and risks mutating schema metadata across transformation passes.

## Decision

1. MUST: Schema transformation processors MUST query and register processed schema instances in the context seen cache to detect cyclical schema references and avoid redundant processing.

## Policy Block

- MUST Schema transformation processors MUST query and register processed schema instances in the context seen cache to detect cyclical schema references and avoid redundant processing.

In scope:
- Internal modules implementing schema-to-schema transformation within the core library.
- Processors and generators handling schema serialization and validation keyword mapping.

Out of scope:
- Runtime schema parsing and validation execution pipelines that do not emit schema specifications.
- External consumer-facing schema definitions outside the core transformation subsystem.

## Rationale

- Adopting the json-schema-processors internal module establishes discrete boundaries for each schema definition type, enabling targeted unit testing and straightforward extensibility.
- Maintaining an explicit seen cache on the traversal context guarantees cycle detection and bounded execution time when resolving complex recursive schemas.
- Isolating default values via serialization round-tripping guarantees that schema metadata mutations do not bleed into original schema definitions or runtime instances.

## Consequences

Positive:
- Schema transformation rules are modularized and testable in isolation from document generation orchestration.
- Cyclic schema references are safely detected and resolved without causing stack overflow errors.
- Default value metadata is safely decoupled from mutable references.

Negative:
- Cross-module indirection increases the number of internal core module dependencies.
- Deep cloning default values via serialization imposes modest runtime allocation overhead during schema generation.

## Alternatives

- Monolithic Generator Transformation Function (rejected)
  Rejected because: Consolidating all schema type transformations inside a single generator function creates unmaintainable cyclomatic complexity and hampers isolated testing.
  When valid: Only in trivial schema systems supporting a small, fixed set of primitive types without recursion.
- Direct Inter-Processor Invocation Architecture (rejected)
  Rejected because: Allowing schema processors to invoke each other directly creates circular module dependencies and bypasses shared traversal context caching.
  When valid: When schemas are strictly hierarchical with no recursive references or shared context requirements.

## Risks

- Circular schema definitions could cause infinite recursion if the traversal context seen cache is bypassed or improperly initialized.
  Mitigation: Enforce strict processor dispatch contracts ensuring every recursive resolution passes through the shared context cache.
  Owner: Core Library Engineering Team
- Serialization round-tripping on default values can fail on non-JSON-serializable data structures.
  Mitigation: Add fallback normalization handling for non-serializable values prior to serialization round-tripping.
  Owner: Core Library Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Processors should be authored as pure functional mappings accepting the schema definition, traversal context, and options.
- Ensure the context seen cache key identity relies on schema definition object references to accurately detect recursive cycles.

## Continuation Context


Verify commands:
- Discover the project test runner script from the root package manifest and execute the core test suite covering schema transformation.
- Inspect the build configuration to identify and run the type-checking and linting verification tasks across core modules.

Accept when:
- All unit tests covering schema transformation processors and generator pipelines execute successfully without regression.
- Cyclic schema references resolve to valid references without triggering call stack exceptions.
- Static type analysis and module linting checks pass with zero reported errors.

## Enforcement

- Verified by: Automated continuous integration pipeline executing unit tests and static analysis.
- Verified by: Mandatory peer code review for changes affecting core schema transformation modules.
- Violation handling: Pull requests bypassing the processor architecture or omitting context cache lookups will fail automated checks and be blocked from merging.
- Violation handling: Identified violations must be refactored to align with modular processor contracts prior to approval.
- Exception process: Architectural exceptions require formal RFC submission and explicit approval from the core library maintainers.
- Exception process: Approved exceptions must be documented alongside justification in the project issue tracker.