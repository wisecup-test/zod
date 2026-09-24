# Core Module Kernel Architecture for Layered Schema Engine Distributions: Engineers Discover Repository Dependency Manifest Lock

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Multiple specialized distribution profiles require access to identical schema parsing logic, standard schema contracts, and serialization protocols.
- Co-locating runtime validation primitives directly within individual distribution entry points causes logic duplication, inconsistent behavior across variants, and circular dependency risks.
- Consolidating foundational registries and execution utilities into a dedicated core module establishes a single source of truth for the validation engine.

## Problem Statement

Maintaining distinct distribution surfaces—such as full-featured compatibility profiles alongside compact execution profiles—leads to fragmented schema parsing routines, duplicated serialization logic, and registry divergence if core mechanics are distributed across surface layers. A decoupled internal core module is required to enforce unidirectional dependency boundaries, unify standard specification adapters, and ensure consistent validation mechanics across all operational variants.

## Decision

1. MUST: Engineers MUST discover the repository dependency manifest and lock artifact to verify the exact resolved version of all external specification libraries before implementing core module integrations.

## Policy Block

- MUST Engineers MUST discover the repository dependency manifest and lock artifact to verify the exact resolved version of all external specification libraries before implementing core module integrations.

In scope:
- Internal runtime modules, parsing utilities, schema registries, and distribution surface profiles.
- Transformations, validations, and standard schema integrations across library distribution variants.

Out of scope:
- End-user consuming applications that interact strictly with published distribution surfaces.
- Standalone localized error message translation dictionaries that do not interact with core schema mechanics.

Exceptions:
- EXC-20-001: A distribution profile requires isolated mock primitives exclusively within isolated unit test environments without initializing the global registry.

## Rationale

- Evidence across eleven distribution and utility files demonstrates consistent inward dependency on the core module, confirming a strictly enforced inward architectural boundary.
- Encapsulating global registry management and standard schema serialization within the core kernel ensures schema identity consistency and identical validation behavior across distribution profiles.
- Unidirectional module dependencies prevent circular reference hazards and reduce overall distribution bundle footprint for lightweight variants.

## Consequences

Positive:
- Eliminates logic drift and duplicate validation mechanics across classic and compact distribution surfaces.
- Enforces a clean unidirectional dependency graph that simplifies tree-shaking and module bundling.
- Centralizes standard schema protocol integration and registry management in a single maintainable boundary.

Negative:
- Modifications to core parsing interfaces necessitate coordinated updates and rigorous regression testing across all dependent distribution surfaces.
- Internal API exposure between the core module and surface profiles requires strict boundary discipline to avoid accidental surface leakage.

## Alternatives

- Monolithic distribution layer where all schema parsing, registries, and surface helpers reside in a single flat package without core separation (rejected)
  Rejected because: Increases bundle overhead for lightweight consumers and prevents clean isolation of standard schema protocols from variant-specific helpers
  When valid: Small libraries with a single entry point and no variant distributions
- Completely independent, duplicated implementations for each distribution profile without a shared core module (rejected)
  Rejected because: Causes synchronization overhead, duplicate bug reproduction, and inevitable behavioral drift between distribution variants
  When valid: Distribution profiles targeting mutually incompatible runtimes with zero shared primitives

## Risks

- Breaking changes in the core kernel cascading into multiple distribution profiles simultaneously
  Mitigation: Maintain explicit semantic interfaces on core exports and mandate automated cross-variant compatibility test suites in continuous integration
  Owner: Core Framework Engineering Team
- Leaking private core module utilities into public consumer-facing type definitions or package manifests
  Mitigation: Configure distribution packaging filters to restrict public visibility strictly to designated distribution facade entry points
  Owner: Release Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Structure internal core exports through a dedicated entry interface to establish a well-defined boundary for surface variants.
- Ensure registry singletons instantiated in the core module maintain strict reference identity across dynamic imports and distribution boundaries.

## Continuation Context


Verify commands:
- Discover the project script runner and execute the module dependency boundary linting suite to verify that no circular dependencies or reverse imports exist from core to distribution surfaces.
- Discover and run the project type-checking and unit test suites across all distribution variants to confirm uniform behavior against core schema utilities.

Accept when:
- The module boundary analysis confirms zero inward imports from the core module to outer distribution variants.
- All distribution test suites pass without registry conflicts or schema parsing discrepancies.

## Enforcement

- Verified by: Continuous integration static analysis checks enforcing architectural import boundaries.
- Verified by: Automated test suites validating behavior across all distribution profiles against the core module.
- Verified by: Peer code review for any pull request modifying core interfaces or exports.
- Violation handling: Pull requests introducing reverse dependencies from core to distribution surfaces are blocked automatically.
- Violation handling: Unauthorized bypass of core module registries will fail architectural linting and must be refactored prior to merge.
- Exception process: Exception requests must be submitted to the architecture review team with technical justification demonstrating why a core abstraction cannot satisfy the variant requirement.