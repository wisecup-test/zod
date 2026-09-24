# Zod Core JSON Schema Generation and Traversal Cache Architecture: Schema Specific Conversion Routines Encapsulate Default

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Translating complex schema structures with circular references, shared definitions, and type checks into standard JSON Schema specifications requires structured traversal management.
- Direct monolithic conversion scripts lead to unmaintainable recursion handling and failure to track visited nodes across deeply nested or recursive types.
- Decoupling transformation orchestration from specialized schema processors ensures distinct schema types are independently maintained while sharing a unified traversal context.
- Employing an explicit seen cache layer within the context guarantees termination on cyclic graphs and enables definition reuse across composite structures.

## Problem Statement

Without a formal separation between schema traversal orchestration and schema-specific processing routines, generating JSON Schema from recursive and multi-layered type systems risks infinite recursion, code duplication, and inconsistent definition referencing. A structured architecture is required to standardize context passing, visited schema caching, and processor delegation across the internal core library.

## Decision

1. SHOULD: Schema-specific conversion routines SHOULD encapsulate default value serialization and property constraints within specialized processor units rather than in the root orchestration module.

## Policy Block

- SHOULD Schema-specific conversion routines SHOULD encapsulate default value serialization and property constraints within specialized processor units rather than in the root orchestration module.

In scope:
- Core schema transformation subsystems generating standard JSON Schema artifacts from defined internal schemas
- Internal processor and generator modules responsible for schema traversal, registry inspection, and check evaluation

Out of scope:
- Runtime schema parsing and direct data validation pipelines that do not emit schema representation structures
- External schema consumers interacting solely with published external library boundaries

Exceptions:
- EXC-20-001: A custom primitive schema possesses no child references and requires direct standalone conversion without maintaining cross-schema cache state

## Rationale

- Decomposing the pipeline into generator orchestration and individual processor units establishes modular extensibility for new schema variants without destabilizing root traversal logic.
- Tracking schema instances via a context-bound identity cache provides deterministic cycle handling, preventing stack overflow exceptions during graph traversal.
- Centralizing registry lookups and standard schema integration through modular contracts decouples conversion routines from the broader validation runtime.

## Consequences

Positive:
- Eliminates infinite recursion bugs when processing cyclic and self-referencing schema topologies
- Enables modular addition and testing of individual schema processors without altering root generator workflows
- Provides consistent JSON Schema output structures through shared registry lookups and cached definitions

Negative:
- Requires strict adherence to passing and propagating context state through all processor invocations
- Increases architectural surface area and internal module indirection relative to a single-pass conversion function

## Alternatives

- Monolithic single-function recursive traversal without a decoupled context cache (rejected)
  Rejected because: Fails to reliably terminate on self-referencing schemas and results in poor code maintainability as schema varieties expand
  When valid: Valid only in small, non-recursive schemas with a fixed and trivial set of primitive types
- Global singleton registry caching across all serialization runs (rejected)
  Rejected because: Causes cross-run state pollution, memory leaks, and concurrency hazards across independent schema generation calls
  When valid: Valid only in completely static, immutable environments where schemas are never dynamically generated at runtime

## Risks

- Processor implementations omitting cache checks could cause runaway recursion on recursive schemas
  Mitigation: Enforce context validation assertions and automated cyclic schema test cases across all registered processors
  Owner: Core Library Engineering Team
- Internal registry schema evolution may drift out of sync with generator expectations
  Mitigation: Validate generator and processor unit tests against the centralized registry definitions in continuous integration
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
- Initialize the traversal context with an empty identity cache at the entry point of the JSON Schema generation pipeline and thread the context immutably through all delegated processors.
- When serializing default values and constraints, ensure deep copies or immutable parsing is applied to prevent unintended mutation of schema definitions.

## Continuation Context


Verify commands:
- Discover and run the project test suite targeting schema serialization and JSON Schema generation modules.
- Discover and execute the type-checking and linter suites to verify module contracts and boundary conformance across core libraries.

Accept when:
- All unit tests covering schema-to-JSON-Schema conversion, including cyclic and recursive schema test suites, pass without regression.
- Traversal context properly records visited schemas and prevents duplicate definition output.
- Static analysis and type validation pass with zero errors across all core modules.

## Enforcement

- Verified by: Automated continuous integration pipelines validating unit tests and recursive schema edge cases
- Verified by: Architectural and peer code reviews for any pull request touching core schema generation or processor modules
- Violation handling: Pull requests bypassing context cache checks or breaking modular separation will be blocked at review
- Violation handling: Failures in recursive schema tests will trigger immediate build failure
- Exception process: Submit an architectural review request detailing the necessity for bypassing context traversal, subject to approval by the core maintainers