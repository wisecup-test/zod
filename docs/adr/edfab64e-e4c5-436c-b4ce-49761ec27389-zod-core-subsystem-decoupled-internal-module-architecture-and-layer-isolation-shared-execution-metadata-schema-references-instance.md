# Zod Core Subsystem: Decoupled Internal Module Architecture and Layer Isolation: Shared Execution Metadata Schema References Instance

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The library implements schema validation, error generation, constraint checking, and specification mapping across multiple functional domains.
- Monolithic module structures risk tight coupling, circular evaluation dependencies, and unnecessary runtime overhead across consumer entry points.
- The codebase establishes a partitioned core layer containing specialized submodules for schemas, checks, errors, registries, and standard protocol integrations, which isolated compatibility facades consume.

## Problem Statement

Maintaining complex schema validation and serialization mechanisms within a single cohesive library requires strict structural boundaries to prevent circular dependencies between schema definitions, validation checks, and error reporting. Without explicit module partitioning and unidirectional layer consumption, changes to internal evaluation routines destabilize external compatibility interfaces and impede granular submodule reusability.

## Decision

1. SHOULD: Shared execution metadata, schema references, and instance caching SHOULD be routed through dedicated registry utilities rather than ambient global state.

## Policy Block

- SHOULD Shared execution metadata, schema references, and instance caching SHOULD be routed through dedicated registry utilities rather than ambient global state.

In scope:
- Implementation of internal schema validation logic, constraint checking, error formatting, and serialization within the core subsystem.
- Authoring compatibility facades, adapters, and schema processor extensions that depend on core validation mechanics.

Out of scope:
- Standalone consumer applications that consume published top-level public package exports.
- Ad-hoc documentation examples and isolated benchmark scripts outside library compilation units.

Exceptions:
- EXC-20-001: A circular reference is fundamentally required by recursive schema definitions at runtime and cannot be decoupled via registry lookups.

## Rationale

- Partitioning schema definitions, validation checks, registries, and error constructs into distinct submodules enforces single-responsibility boundaries and eliminates cyclic evaluation hazards.
- Directing higher-level compatibility facades to depend strictly downward onto core abstractions ensures API stability while allowing underlying engine mechanics to evolve independently.
- Centralizing reference resolution and prototype tracking within dedicated registries enables deterministic caching without leaking internal state across disparate module files.

## Consequences

Positive:
- Clear architectural boundaries prevent circular dependency deadlocks between schema declarations and validation checks.
- Fine-grained submodule partitioning supports tree-shaking and enables focused unit testing of discrete subsystem capabilities.
- Compatibility facade layers can maintain legacy surfaces while delegating core parsing and validation to unified internal engines.

Negative:
- Developers must navigate multiple submodule boundaries and explicit import paths rather than consuming a single internal module.
- Managing cross-submodule registries increases initial setup complexity for shared state and recursion resolution.

## Alternatives

- Monolithic Internal Module (rejected)
  Rejected because: Co-locating schema declarations, execution checks, registry state, and error handling in a single internal bundle creates severe coupling and cyclic evaluation loops.
  When valid: Small utility libraries containing few interconnected schema types with zero third-party compatibility facades.
- Decentralized Ad-Hoc Module Coupling (rejected)
  Rejected because: Allowing arbitrary bi-directional imports between compatibility layers and core mechanics results in architectural erosion and brittle release surfaces.
  When valid: Prototyping exploratory spike projects prior to formalizing library architecture.

## Risks

- Submodule boundary proliferation may lead to inconsistent import conventions and fragmented shared registries.
  Mitigation: Enforce strict unidirectional dependency rules and automated module boundary linting during build verification.
  Owner: Library Architecture Team
- Drift between core internal contracts and compatibility facades could cause regression in consumer-facing APIs.
  Mitigation: Execute full regression test suites and type-compatibility verification across both core and compatibility layers.
  Owner: Quality Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Organize internal core capabilities into discrete functional submodules focused strictly on single domains such as checks, errors, schemas, registries, and protocol adapters.
- Ensure registry lookup patterns handle recursive references lazily to maintain deterministic execution order during schema composition.

## Continuation Context


Verify commands:
- Discover and execute the project static analysis and linting scripts to verify that module dependency boundaries and import directions adhere to architectural constraints.
- Discover and run the project test suite across all workspace packages to ensure cross-module compatibility and validation parity.
- Inspect the project lock resolution artifact to verify that all referenced dependencies match the authoritative pinned versions.

Accept when:
- All internal module imports follow unidirectional downward layering from facade modules to core modules without circular references.
- Project static analysis and unit test suites execute and pass with zero boundary violations.
- Schema registry resolution and validation pipelines execute deterministically across all test suites.

## Enforcement

- Verified by: Continuous integration automated linting and dependency tree boundary checks.
- Verified by: Peer code review mandatory approval for architectural imports across module boundaries.
- Violation handling: Automated build failure on detected circular imports or unauthorized upward dependencies from core modules.
- Violation handling: Pull request rejection pending resolution of architectural boundary violations.
- Exception process: Submit an architectural review request detailing technical necessity and proposed mitigation for temporary circular or ad-hoc bindings.