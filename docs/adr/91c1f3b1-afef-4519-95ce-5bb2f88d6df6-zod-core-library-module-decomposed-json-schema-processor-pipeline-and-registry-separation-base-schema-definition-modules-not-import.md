# Zod Core Library Module: Decomposed JSON Schema Processor Pipeline and Registry Separation: Base Schema Definition Modules Not Import

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The core library engine requires comprehensive schema transformation capabilities into standard external representations such as JSON schema without creating monolithic transformation units.
- Schema representations can include deeply nested, mutually recursive, and cyclical structures that require dedicated traversal caching to prevent infinite loops.
- Separating schema definitions, validation checks, global metadata registries, and target format processors ensures clear domain boundaries within the internal library structure.
- Introspection and serialization workflows must query schema metadata and registry entries without binding base schema runtime definitions directly to serialization schemas.

## Problem Statement

Directly embedding serialization and JSON schema generation logic within core schema definition classes couples runtime validation mechanics to external schema representation formats, complicates recursive cycle handling, and leads to sprawling, tightly coupled transformation code.

## Decision

1. MUST_NOT: Base schema definition modules MUST NOT import downstream serialization processors or schema generation coordinators, preserving unidirectional dependency flow from serializers to core schemas.

## Policy Block

- MUST_NOT Base schema definition modules MUST NOT import downstream serialization processors or schema generation coordinators, preserving unidirectional dependency flow from serializers to core schemas.

In scope:
- Internal core library modules implementing schema transformations, serialization pipelines, and metadata registries.
- Subsystems performing structural traversal and external schema generation on core schema instances.

Out of scope:
- Consumer application schemas that interact exclusively with the public library facade.
- Standalone primitive validation check functions that do not participate in schema graph traversal.

Exceptions:
- EXC-20-001: Lightweight non-recursive primitive serialization that does not require registry lookup or cycle detection context

## Rationale

- Decomposing JSON schema generation into dedicated generator coordinators and processor modules establishes clear separation of concerns, allowing serialization logic to evolve independently from core validation mechanics.
- Decoupled traversal context tracking using seen maps reliably breaks cyclical object references, preventing recursion overflow without leaking traversal bookkeeping into schema instances.
- Centralizing metadata lookups within dedicated registry abstractions decouples schema definitions from downstream consumer extensions and cross-cutting tool bindings.

## Consequences

Positive:
- Enforces unidirectional dependencies from format serializers toward core schema representations.
- Guarantees cycle safety and deterministic reference generation during complex recursive schema transformations.
- Facilitates independent unit testing and extension of format-specific processor routines without modifying runtime validation schemas.

Negative:
- Increases call stack depth and requires propagating traversal context across multiple dispatch layers.
- Requires maintaining bidirectional coordination between processor registries and dynamic schema dispatchers.

## Alternatives

- Monolithic Schema Visitor Method on Schema Base Classes (rejected)
  Rejected because: Embedding serialization methods directly into base schema classes bloats runtime definitions with serialization dependencies and creates circular module dependencies.
  When valid: Simple libraries with minimal schema types and no recursive or cyclic reference requirements.
- Decoupled Processor Pipeline with Contextual Registry Separation (accepted)
  Rejected because: N/A - Adopted architectural design.
  When valid: Complex schema validation systems supporting cyclic structures, registries, and extensible format conversions.

## Risks

- State pollution or memory retention if traversal context caches outlive individual transformation operations.
  Mitigation: Ensure traversal context instances are scoped strictly to the lifecycle of a single root generation call.
  Owner: Engineering team
- Missing processor registrations for new schema types leading to runtime transformation failures.
  Mitigation: Enforce exhaustive processor mapping in verification test suites to detect unmapped schema definitions.
  Owner: Engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Instantiate a fresh traversal context for each top-level transformation invocation, passing the context reference through child processor functions to record visited instances.
- Query the centralized schema registry for auxiliary metadata such as titles, descriptions, and custom keywords before emitting generated schema nodes.

## Continuation Context


Verify commands:
- Discover and execute the project test runner script defined in the project configuration to validate schema transformation behaviors and processor test suites.
- Execute the static type checking and modular dependency validation suites configured in the repository to guarantee unidirectional module dependencies.
- Run the repository linter and architecture boundary checks defined in project configuration to verify adherence to module import boundaries.

Accept when:
- All test suites covering schema serialization, cycle detection, and registry lookups pass with zero errors.
- Dependency verification confirms no circular dependencies exist between schema definitions and serialization processors.
- Static analysis confirms all schema types have corresponding registered transformation handlers.

## Enforcement

- Verified by: Automated continuous integration checks executing repository test and validation scripts.
- Verified by: Peer code review verifying adherence to processor isolation and context management constraints.
- Violation handling: Pull requests introducing circular dependencies between schemas and processors will be blocked by continuous integration.
- Violation handling: Code directly mutating schema definitions for serialization tracking must be rejected during code review.
- Exception process: Propose an architectural deviation to the core library maintenance team detailing why an isolated processor pattern is insufficient.
- Exception process: Obtain formal approval from library maintainers and document the exemption in the affected module.