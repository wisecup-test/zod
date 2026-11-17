---
version: 2
name: 5d6c8f0c-3092-41db-b9f2-ea9b8c96387c-internal-schema-metadata-registries-module-for-contextual-state-and-bidirectional-identity-storage-internal-registries-module-serve-authoritative-data
description: "Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Internal Registries Module Serve Authoritative Data"
metadata:
  actual:
    adr_id: 5d6c8f0c-3092-41db-b9f2-ea9b8c96387c
    status: accepted
    candidate_group_id: d8b3ef21-85e1-4a50-9fc9-84f24d157d45
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
      - src/v4/**
---

# Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Internal Registries Module Serve Authoritative Data

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v3/**`
- `src/v4/**`

## Context

- Schema processing pipelines require associating schema definitions with external identifiers, tracking circular references during serialization, and managing intermediate compilation constants across transformation phases.
- Mutating schema definitions directly to store contextual metadata introduces side effects, violates immutability guarantees, and degrades cache coherence across independent transformations.
- The internal schema metadata registry module isolates schema-to-metadata associations and bidirectional identifier indices into dedicated registry structures with explicit lifecycle boundaries.
- Contextual traversal structures maintain transient state collections across schema transformation and compilation operations, cleaning up tracking references upon scope exit.

## Problem Statement

Schema compilation, serialization, and deserialization routines require attaching external metadata and managing cyclic reference state without mutating underlying schema definitions or leaking memory across traversal lifecycles.

## Decision

1. MUST: The internal registries module MUST serve as the authoritative data access abstraction for associating schema definitions with external metadata and bidirectional identifier mappings.

## Policy Block

- MUST The internal registries module MUST serve as the authoritative data access abstraction for associating schema definitions with external metadata and bidirectional identifier mappings.

In scope:
- Schema metadata association and external identifier resolution.
- Recursive schema serialization and deserialization involving circular reference tracking.
- Compiler constant registration and variable scope isolation during schema code generation.

Out of scope:
- Direct evaluation of primitive type guards without metadata associations.
- Stateless in-memory scalar validations requiring no cross-schema reference traversal.

Exceptions:
- EXC-30-001: Transient inlined union checks execute in isolated single-pass evaluators without cyclic references or external identifiers.

## Rationale

- Decoupling schema identity and metadata storage via dedicated registry structures ensures that schema definitions remain strictly immutable and thread-safe across concurrent validations.
- Explicit deletion of tracking entries during recursive traversal mitigates memory retention risks that arise when caching visited nodes in deeply nested schemas.
- Dual-indexed registry lookups provide constant-time resolution between schemas and unique identifiers, eliminating linear array traversals during schema emission.

## Consequences

Positive:
- Preserves schema immutability by preventing contextual and traversal metadata from polluting schema definition objects.
- Enables cycle-safe recursive schema transformations through structured lookup and recursion tracking containers.
- Provides deterministic cleanup of traversal state during compilation and schema translation phases.

Negative:
- Requires developers to thread explicit context containers through every level of recursive visitor calls in schema transformations.
- Introduces operational overhead for maintaining synchronization across dual primary and secondary index collections.

## Alternatives

- Direct Schema Instance Property Mutation (rejected)
  Rejected because: Mutating schema objects directly breaks immutability guarantees, introduces race conditions and cross-talk during concurrent validations, and leads to memory leaks across recurring runs.
  When valid: Single-threaded throwaway evaluation scripts where schema instances are discarded immediately after a single execution.
- Global Unscoped WeakMap Caching (rejected)
  Rejected because: Global WeakMaps cannot support serializable string identifier reverse lookups without object keys and do not provide deterministic lifecycle scoping for transient recursion markers.
  When valid: Purely garbage-collected caching of derived properties where inverse string identifier resolution is not required.

## Risks

- Desynchronization between primary schema maps and secondary identifier lookup maps during partial deregistration.
  Mitigation: Encapsulate deletion operations inside atomic registry methods that purge both indices within a single method call.
  Owner: engineering team
- Memory retention caused by neglected deletion calls in traversal contexts during exceptional termination.
  Mitigation: Wrap recursive traversal calls in structured exception-handling blocks that guarantee cleanup upon completion.
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
- Instantiate traversal contexts at the root of translation or compilation workflows and pass context instances explicitly down recursive visitor calls.
- Implement bidirectional registry collections with unified registration methods that set both object-keyed and string-keyed associations concurrently.

## Continuation Context


Verify commands:
- Discover the workspace test execution script in the project manifest and run the suite covering schema registries and compiler traversal.
- Discover the repository static analysis script and verify zero direct property mutations on schema instances across data access modules.

Accept when:
- All registry unit and integration test suites pass with complete assertion coverage on bidirectional lookup, registration, and deletion.
- Memory profiling tests confirm traversal context maps release all tracking references upon traversal completion without leakage.
- Static type checks verify that schema definitions remain read-only and all external metadata access occurs through registry abstractions.

## Enforcement

- Verified by: Automated unit and integration test runs executed during continuous integration workflows.
- Verified by: Peer code reviews auditing registry data access patterns and recursion cleanup logic.
- Verified by: Static analysis checks detecting unauthorized property assignments to schema definition objects.
- Violation handling: Code review rejection for pull requests that mutate schema instances directly to store state.
- Violation handling: Automated continuous integration failures when bidirectional registry indices fail synchronization invariants.
- Exception process: Submit an architectural review request detailing why registry-based access is impractical for the specific isolated evaluation path.
- Exception process: Obtain explicit sign-off from the technical lead with documented memory profiling and immutability impact assessments.