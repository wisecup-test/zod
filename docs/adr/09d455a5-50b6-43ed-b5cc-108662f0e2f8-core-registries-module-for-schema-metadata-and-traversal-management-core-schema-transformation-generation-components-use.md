---
version: 2
name: 09d455a5-50b6-43ed-b5cc-108662f0e2f8-core-registries-module-for-schema-metadata-and-traversal-management-core-schema-transformation-generation-components-use
description: "Core Registries Module for Schema Metadata and Traversal Management: Core Schema Transformation Generation Components Use"
metadata:
  actual:
    adr_id: 09d455a5-50b6-43ed-b5cc-108662f0e2f8
    status: accepted
    candidate_group_id: 030063b8-d655-44ea-bf21-c6f9f8fd93bf
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Registries Module for Schema Metadata and Traversal Management: Core Schema Transformation Generation Components Use

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/core/**`

## Context

- Complex schema transformation and serialization pipelines require tracking schema identity, associated metadata, and visited nodes across deeply nested or recursive definitions.
- Attaching metadata and cycle-detection state directly onto schema instance payloads causes object shape mutation, memory leaks, and serialization interference.
- Decoupled registry services allow core schema definitions to remain immutable while providing centralized lookup and scoped context caches during schema traversal.

## Problem Statement

Transforming schema structures into target specifications requires resolving associated metadata and handling cyclic schema structures without mutating immutable schema instances. Lacking a centralized registry and context-bound traversal cache leads to fragmented metadata storage, duplicate object processing, and recursion runtime errors.

## Decision

1. MUST: Core schema transformation and generation components MUST use the internal registries module for global schema registration and metadata resolution.

## Policy Block

- MUST Core schema transformation and generation components MUST use the internal registries module for global schema registration and metadata resolution.

In scope:
- Core schema transformation pipelines
- Schema serialization and generation modules
- Internal API schema instance registries

Out of scope:
- Stateless primitive validation operations
- External consumer application logic

Exceptions:
- EXC-20-001: Isolated unit testing of schema nodes where metadata resolution is not evaluated

## Rationale

- Centralizing instance tracking in globalRegistry ensures singular instance identity across modular boundaries.
- Contextual caching via ctx.seen safely manages recursive and cyclical schema definitions during tree traversal without mutating input instances.
- Separating metadata via metadataRegistry decouples schema definition data structures from consumer-specific or target-specific annotations.

## Consequences

Positive:
- Guarantees immutability of schema definitions during transformations and conversions.
- Prevents infinite recursion and call-stack overflow exceptions in cyclical schema structures.
- Provides deterministic and centralized metadata lookup across disparate processing stages.

Negative:
- Requires threading explicit execution context objects through all downstream visitors and schema processors.
- Increases memory overhead during deep schema traversal due to retained context cache references.

## Alternatives

- In-place schema instance mutation with transient traversal flags (rejected)
  Rejected because: Mutating schema definition instances violates object immutability and introduces race conditions across concurrent schema transformations.
  When valid: Single-threaded throwaway scripts without shared instance references.
- Decoupled external symbol properties attached directly to schema instances (rejected)
  Rejected because: Symbol properties still alter underlying schema objects and cause memory retention if not manually cleared after traversal.
  When valid: Lightweight single-pass traversals without centralized metadata mapping requirements.

## Risks

- Memory leaks in long-lived contexts if traversal cache references are not cleared post-execution
  Mitigation: Scope traversal contexts strictly to individual transformation calls and rely on garbage collection of ephemeral contexts.
  Owner: Core Library Engineering Team
- Cache collisions or stale reads when schema instances share identical serialized signatures
  Mitigation: Key traversal caches by object reference rather than structural hashing.
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
- Instantiate execution context instances at the root of schema processing and pass the context reference to all downstream visitors.
- Ensure identity registries use reference-equality data structures to prevent unintended duplicate entries for equivalent schema definitions.

## Continuation Context


Verify commands:
- Discover and run the project test suite covering core schema transformation and registry operations.
- Discover and run the repository static analysis and type checking verification scripts.

Accept when:
- All core schema transformation tests pass without circular reference errors.
- Static analysis confirms that metadata resolution and traversal state operations use the designated registries and context APIs.

## Enforcement

- Verified by: Automated continuous integration test and static analysis suites
- Verified by: Peer code review for core schema processing pull requests
- Violation handling: Pull requests mutating schema instances or bypassing registries are blocked from merging
- Violation handling: Flagged violations must be refactored to use context registries
- Exception process: Submit an architectural review request detailing why context registry usage is technically infeasible for the specific transform.