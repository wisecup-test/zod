---
version: 2
name: 6b7a2cdd-0c19-4726-b25f-09465eea8336-core-module-architecture-for-validation-engine-and-global-registry-management-compatibility-adapters-external-schema-converters-delegate
description: "Core Module Architecture for Validation Engine and Global Registry Management: Compatibility Adapters External Schema Converters Delegate"
metadata:
  actual:
    adr_id: 6b7a2cdd-0c19-4726-b25f-09465eea8336
    status: accepted
    candidate_group_id: d439e3f0-eafd-4b71-a843-e881f89e04eb
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/**
---

# Core Module Architecture for Validation Engine and Global Registry Management: Compatibility Adapters External Schema Converters Delegate

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `packages/zod/src/v4/**`

## Context

- Schema evaluation, registry tracking, and error reporting systems require modular organization to decouple foundational validation logic from specialized transformations and compatibility interfaces.
- The codebase establishes an internal core module partition providing canonical definitions for schemas, checks, errors, and global registry access across distinct library sub-layers.
- Compatibility layers and external schema converters consume these foundational primitives through explicit internal module contracts rather than duplicating runtime validation primitives.

## Problem Statement

Tightly coupling schema evaluation, serialization mappings, and backward-compatibility layers creates circular dependencies, bloats consumer runtime bundles, and complicates state synchronization across schema registries. The project requires a partitioned internal core module structure that isolates primitive validation checks, error representations, and global registry services from transformation processors and public facade interfaces.

## Decision

1. SHOULD: Compatibility adapters and external schema converters SHOULD delegate directly to core registry lookups and standard schema protocols to preserve uniform parsing semantics.

## Policy Block

- SHOULD Compatibility adapters and external schema converters SHOULD delegate directly to core registry lookups and standard schema protocols to preserve uniform parsing semantics.

In scope:
- Implementation and extension of validation schemas, checks, and error structures.
- Registration and resolution of schema metadata within internal registries.
- Integration of schema transformation processors and legacy compatibility adapters.

Out of scope:
- Third-party application code integrating the public validation library facade without extending core modules.
- Isolated unit test fixtures that do not interact with shared registry instances.

## Rationale

- Centralizing primitive schema evaluation, checks, and error structures within a dedicated core module eliminates circular dependencies and preserves unidirectional dependency flows.
- Operating a unified global registry across core and compatibility layers guarantees consistent metadata inspection across independent schema instances.
- Separating core primitives from transformation engines ensures consumer modules only incur runtime weight for the schema capabilities they directly reference.

## Consequences

Positive:
- Provides clear architectural boundaries that prevent coupling between primitive validation mechanics and specialized schema converters.
- Unifies metadata resolution and instance tracking through a single global registry interface.
- Allows independent testing and maintenance of foundational validation checks and error utilities.

Negative:
- Increases import path indirection across multi-layer module boundaries.
- Requires strict enforcement of dependency hierarchy to prevent accidental backward imports from compatibility layers into core modules.

## Alternatives

- Monolithic single-namespace module bundling all schemas, transformations, and compatibility logic (rejected)
  Rejected because: Induces high bundle size overhead, tightly couples unrelated schema transformation formats, and introduces circular dependency hazards.
  When valid: Small libraries where minimal footprint and unified single-file simplicity outweigh modularity requirements.
- Completely decoupled peer packages with independent registry state (rejected)
  Rejected because: Splits schema registry state across package boundaries, resulting in metadata cache misses and incompatible schema instance resolution.
  When valid: Fully autonomous domain libraries that do not share underlying schema instance graphs.

## Risks

- Circular dependency leakage between core validation primitives and compatibility adapters
  Mitigation: Automated linting rules and structural dependency analysis executed during continuous integration to detect prohibited imports.
  Owner: Architecture and Library Infrastructure Team
- Memory retention from unregistered or persistent schema instances within the global registry
  Mitigation: Structured registry life-cycle management and weak referencing patterns where supported.
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
- Organize internal imports so that dependent compatibility and transformation layers access core modules via relative boundary entry points without circumventing internal directory scoping.
- When extending schema parsing behavior, implement custom validation logic as discrete check primitives within the core layer before registering public schema methods.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting command to verify module boundary compliance.
- Discover and execute the project test runner across core module test suites.
- Discover and execute the circular dependency checker script defined in the project configuration.

Accept when:
- All core module test suites complete with zero errors.
- Static dependency validation passes without detecting disallowed inward imports into the core module layer.
- Schema registry resolution tests verify deterministic cache lookups across compatibility facades.

## Enforcement

- Verified by: Automated dependency graph validation and static lint checks executed in continuous integration pipelines.
- Verified by: Peer code review mandatory for any changes altering core module interfaces or registry structures.
- Violation handling: Pull requests introducing backward dependencies into core modules or circumventing the global registry are automatically blocked.
- Violation handling: Architectural violations must be refactored to comply with core module boundaries prior to merge approval.
- Exception process: Exceptions require formal architectural review and written consensus from library maintainers documenting why the dependency boundary cannot be maintained.