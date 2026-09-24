# Zod Core Module Architecture and Registry Separation: Schema Serialization Processors Deserialization Routines Interface

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Schema validation systems require strict isolation between fundamental parsing pipelines, error reporting structures, and outer integration facades to prevent circular dependencies and state leakage.
- High-performance schema operations require dedicated metadata registries that associate schema instances with identifiers and serialization descriptors without mutating underlying schema definitions directly.
- Maintaining compatibility layers alongside modernized internal validation primitives necessitates clean internal module boundaries where outer compatibility modules consume decoupled core utilities and schemas.

## Problem Statement

Coupling schema execution, error formatting, check evaluations, and metadata caching into a monolithic interface creates circular dependencies, hinders modular tree-shaking, and tightly couples serialization mechanisms to specific schema representations.

## Decision

1. SHOULD: Schema serialization processors and deserialization routines SHOULD interface with schema definitions strictly through public registry lookups and standard schema interfaces.

## Policy Block

- SHOULD Schema serialization processors and deserialization routines SHOULD interface with schema definitions strictly through public registry lookups and standard schema interfaces.

In scope:
- Core schema definition, execution, parsing, check processing, and error handling modules.
- Metadata registries, serialization mapping layers, and compatibility facade integrations.

Out of scope:
- Standalone peripheral plugins or external application code operating outside the library core architecture.
- Third-party application-level business schemas that interact exclusively with public library interfaces.

Exceptions:
- EXC-20-001: Performance-critical validation paths require direct internal reference access bypassing registry lookup tables under verified microbenchmark constraints.

## Rationale

- Decoupling core schema evaluation, error structures, and checks into an isolated core layer establishes clear unidirectional dependency boundaries across fourteen core modules.
- Implementing dedicated schema registries to manage identifiers and metadata prevents prototype pollution, enables bidirectional reference resolution, and supports recursive schema serialization.
- Isolating compatibility wrappers and format processors from core execution mechanics allows independent iteration and optimization of runtime validation engines without breaking consumer contracts.

## Consequences

Positive:
- Prevents circular dependencies across validation, parsing, error creation, and transformation modules.
- Enables centralized reference tracking and cyclic structure handling during schema serialization and deserialization via dedicated registries.
- Maintains backwards compatibility through decoupled outer facades while keeping internal execution engines minimal and cohesive.

Negative:
- Requires explicit registry synchronization and lifecycle management to prevent memory retention of unreferenced schema instances.
- Introduces intermediate registry lookups and boundary indirection across serialization pipelines.

## Alternatives

- Monolithic schema class hierarchy embedding metadata, parsing, serialization, and legacy methods directly on schema instances (rejected)
  Rejected because: Creates high cyclomatic complexity, introduces circular dependencies between schemas and serializers, and prevents tree-shaking
  When valid: Small libraries with trivial schema types and no external format serialization requirements
- Decoupled functional pipeline architecture separating core engines and external registries (accepted)
  Rejected because: None; aligns with observed multi-module decoupling and metadata registry isolation
  When valid: Complex validation libraries supporting diverse schemas, recursive reference resolution, and multiple serialization targets

## Risks

- Memory leaks caused by retaining schema references in internal registry lookup maps across extended runtimes
  Mitigation: Implement weak references or explicit lifecycle deletion routines when schemas and associated identifiers are deregistered
  Owner: Core Library Maintainers
- Circular dependency reintroduction during cross-module feature additions between parsing, checks, and utilities
  Mitigation: Automate architectural boundary validation in static analysis checks to enforce strict unidirectional module hierarchy
  Owner: Core Library Maintainers

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Implement metadata registries using bidirectional mapping structures that associate schema objects with string identifiers while providing symmetric deletion operations.
- Ensure compatibility modules import core functionality strictly through designated entrypoints without referencing deep internal implementation modules.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and dependency linting suite from repository configuration scripts to verify unidirectional module imports.
- Discover and execute the internal architecture boundary test suite to ensure no circular references exist between core modules and compatibility layers.

Accept when:
- Static module dependency checks pass without circular dependency violations or illegal cross-boundary imports.
- Schema registry test suites confirm correct bidirectional mapping, cache invalidation, and reference resolution without memory leakage.

## Enforcement

- Verified by: Automated continuous integration pipeline running static module boundary analyses and cyclic dependency checks.
- Verified by: Peer review by core architecture maintainers for any modifications to module import structures or registry lifecycle semantics.
- Violation handling: Pull requests introducing circular module imports, bypassing metadata registries, or violating core boundaries are blocked from merging.
- Exception process: Exceptions require formal submission to the core engineering team with benchmark data demonstrating necessity and a migration plan to restore architectural boundaries.