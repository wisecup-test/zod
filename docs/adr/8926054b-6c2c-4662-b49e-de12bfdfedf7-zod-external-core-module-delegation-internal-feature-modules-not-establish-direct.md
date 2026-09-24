# Zod External Core Module Delegation: Internal Feature Modules Not Establish Direct

Status: proposed
Date: 2025-05-14
Deciders: Detection Pipeline (automated)

## Context

- Multiple variant entry surfaces within the Zod package require access to unified core library capabilities.
- Defining library capabilities independently within each entry facade leads to synchronization overhead, inconsistent export signatures, and duplicated module initialization logic.
- Static intermediate representation analysis identifies consistent delegation to a dedicated external core module across entry boundaries.
- Centralizing shared core functionality behind an external module establishes an explicit abstraction boundary between public entry points and internal library implementations.

## Problem Statement

Multi-surface library distributions risk export divergence and redundant definitions when variant entry points manage their own core implementations. The library requires a cohesive structural convention that isolates shared core primitives into a single internal external module, ensuring consistent API exposure across all public entry facades without duplicating core runtime constructs.

## Decision

1. SHOULD_NOT: Internal feature modules SHOULD_NOT establish direct circular dependencies back to entry point facades that re-export the external module.

## Policy Block

- SHOULD_NOT Internal feature modules SHOULD_NOT establish direct circular dependencies back to entry point facades that re-export the external module.

In scope:
- Entry point modules exposing consumer-facing library surfaces across package variants.
- Core module interface boundaries connecting external facades to internal definitions.

Out of scope:
- Standalone internal utility modules that operate independently of public entry facades.
- Isolated test fixtures and mock environments not published as entry targets.

## Rationale

- Delegating entry point exports to a centralized external module guarantees behavioral parity across distinct distribution variants.
- Isolating core implementations simplifies maintenance by establishing a single source of truth for library definitions.
- Static intermediate representation analysis shows uniform adherence to external module delegation across all observed package entry points with high significance.

## Consequences

Positive:
- Eliminates duplicate runtime logic and export discrepancies across package entry variants.
- Streamlines bug fixes and core enhancements by isolating shared behaviors within a single module boundary.
- Enforces explicit architectural boundaries between consumer entry facades and internal library mechanisms.

Negative:
- Creates architectural coupling between entry facade modules and the internal contract of the external module.
- Requires structural coordination across all entry surfaces whenever the external module interface changes.

## Alternatives

- Independent Core Implementations per Entry Facade (rejected)
  Rejected because: Implementing core constructs separately within each entry module causes API drift, duplicated maintenance overhead, and higher risk of behavioral inconsistencies.
  When valid: When entry variants have completely disjoint domain requirements and share zero common runtime structures.
- Direct Monolithic Inlining in a Single Root Entry (rejected)
  Rejected because: Inlining all functionality into a single root entry prevents tree-shaking and disallows offering specialized or minimal entry variants.
  When valid: When a library publishes exactly one monolithic entry point with no requirements for specialized variant surfaces.

## Risks

- Breaking changes to the external module contract propagate across all entry point facades simultaneously.
  Mitigation: Maintain comprehensive automated interface contract validation across all entry point surfaces during pipeline checks.
  Owner: engineering team
- Unintended inclusion of non-essential core exports can inflate bundle sizes in lightweight entry variants.
  Mitigation: Enforce explicit export gating and selective re-exporting boundaries in specialized entry facades.
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
- Discover module resolution configurations and entry manifests from the repository to map all published export targets to their corresponding core delegations.
- Verify that specialized or compact entry facades import only necessary submodules from the external module to preserve minimal footprint constraints.

## Continuation Context


Verify commands:
- Discover and run the project static analysis suite to verify that all entry modules import shared definitions from the external core module.
- Discover and execute the package boundary and circular dependency verification scripts from repository manifests.
- Discover and run the integration test suite to validate API compatibility across all entry facade surfaces.

Accept when:
- All published entry surfaces successfully delegate core definitions to the external core module without local reimplementation.
- Static analysis and dependency boundary checks complete with zero unresolved imports or circular references.
- All unit and integration verification suites pass across all entry point variants.

## Enforcement

- Verified by: Automated dependency linting and architecture verification checks in the continuous integration pipeline.
- Verified by: Peer code review verification for any changes affecting package entry facades or external core module boundaries.
- Violation handling: Automated continuous integration pipeline failures blocking merge for direct reimplementations of core functions in entry facades.
- Violation handling: Mandatory architectural review and refactoring required before merging changes that bypass the external core module.
- Exception process: Formal architecture review and approval documented in the project tracking system detailing the specific constraints requiring a divergent entry implementation.