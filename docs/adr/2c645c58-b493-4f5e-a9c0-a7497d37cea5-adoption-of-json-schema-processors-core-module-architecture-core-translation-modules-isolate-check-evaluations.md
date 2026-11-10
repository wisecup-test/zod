---
version: 2
name: 2c645c58-b493-4f5e-a9c0-a7497d37cea5-adoption-of-json-schema-processors-core-module-architecture-core-translation-modules-isolate-check-evaluations
description: "Adoption of json-schema-processors Core Module Architecture: Core Translation Modules Isolate Check Evaluations"
metadata:
  actual:
    adr_id: 2c645c58-b493-4f5e-a9c0-a7497d37cea5
    status: accepted
    candidate_group_id: 4f3aa984-f581-4fab-b688-1e6017994f30
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Adoption of json-schema-processors Core Module Architecture: Core Translation Modules Isolate Check Evaluations

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `packages/zod/src/v4/core/**`

## Context

- Schema generation and transformation across diverse schema types requires structured delegation to prevent cyclic dependencies and monolithic generator functions.
- The schema conversion pipeline utilizes dedicated internal core modules including schema processors, generator routines, registries, checks, and translation utilities.
- Recursive schema topologies require reference memoization and visited-node tracking via context caches to prevent infinite loops during traversal.
- Default values and serialized schema attributes require isolated sanitization during the transformation lifecycle.

## Problem Statement

Inline schema-to-JSON-schema conversions create tight coupling between schema definitions and serialization formats, leading to bloated core definitions, duplicated validation logic, and unbounded recursion when processing self-referential or cyclic schemas.

## Decision

1. SHOULD: Core translation modules SHOULD isolate check evaluations, registries, and schema processors into independent modular boundaries within the core subsystem.

## Policy Block

- SHOULD Core translation modules SHOULD isolate check evaluations, registries, and schema processors into independent modular boundaries within the core subsystem.

In scope:
- Core schema-to-JSON-schema transformation and generation modules within the library.
- Validation check routines and registries interacting with schema translation pipelines.

Out of scope:
- Client-side runtime parsing and direct value validation outside schema serialization pipelines.
- External schema format conversions handled by third-party companion extensions.

## Rationale

- Separating schema processing into dedicated core processor modules decouples core schema definitions from export format specifications.
- Contextual tracking using ctx.seen prevents recursion traps and ensures linear traversal performance across deeply nested or cyclic schema graphs.
- Decoupling registries and checks into dedicated core modules enables targeted tree-shaking and simplifies unit testing of isolated schema processors.

## Consequences

Positive:
- Eliminates circular reference failures during JSON schema synthesis through context-bound node tracking.
- Centralizes schema conversion rules in dedicated processor modules, avoiding code duplication across disparate schema definitions.
- Clarifies subsystem boundaries between core validation definitions, type registries, and schema output generators.

Negative:
- Increases indirection across the core subsystem by distributing conversion logic across separate processor and generator modules.
- Incurs memory overhead from maintaining traversal state and cloned object structures in the transformation context.

## Alternatives

- Inline JSON Schema Generation Methods on Schema Class Definitions (rejected)
  Rejected because: Couples core validation classes directly to external schema formats and bloats runtime bundles with serialization logic.
  When valid: Small monolithic libraries where schema definitions are strictly static and non-recursive.
- Monolithic Generator Function with Large Conditional Switch Blocks (rejected)
  Rejected because: Results in unmaintainable single-routine architectures that impede modular extension and complicate individual check processor testing.
  When valid: Trivial schemas supporting a small, fixed number of primitive scalar types.

## Risks

- Cache key collisions or improper cache lifetime management in ctx.seen causing stale schema representations.
  Mitigation: Scope cache instances strictly to the duration of a single schema generation operation lifecycle.
  Owner: Core Engineering Team
- Deep serialization overhead during default value cloning impacting high-throughput schema generation.
  Mitigation: Restrict deep cloning strictly to non-primitive default value nodes that require mutation isolation.
  Owner: Core Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Ensure all schema processor additions implement the standard traversal context interface and propagate the seen-node cache across recursive calls.
- Verify that newly introduced schema checks and registry entries maintain bidirectional compatibility with existing processor definitions.

## Continuation Context


Verify commands:
- Discover and run the project repository validation suite for core module type-checking and unit test suites.
- Discover and execute the repository integration test suite verifying JSON schema generation across complex and cyclic schema fixtures.

Accept when:
- All unit tests for schema processors and generators pass without errors or circular reference exceptions.
- Static type analysis across all core modules completes with zero diagnostic warnings or type mismatch errors.

## Enforcement

- Verified by: Automated continuous integration pipeline running test suites and static analysis verification.
- Verified by: Peer code review mandatory for all modifications touching core schema processor or generator modules.
- Violation handling: Pull requests containing inline schema conversion logic or bypassing the traversal cache are blocked from merging.
- Exception process: Exceptions require formal architectural review and approval by the core library maintainers documented in an ADR amendment.