---
version: 2
name: 67b66d88-47fd-488f-ac96-add3488ae188-in-memory-schema-registry-and-reference-cache-via-registries-module-schema-metadata-access-reference-resolution-route
description: "In-Memory Schema Registry and Reference Cache via Registries Module: Schema Metadata Access Reference Resolution Route"
metadata:
  actual:
    adr_id: 67b66d88-47fd-488f-ac96-add3488ae188
    status: accepted
    candidate_group_id: 28ad3438-82c5-474c-b774-4a2f09b5817d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/**
---

# In-Memory Schema Registry and Reference Cache via Registries Module: Schema Metadata Access Reference Resolution Route

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `packages/zod/src/**`

## Context

- Schema processing and transformation workflows require associating metadata with schema definitions and resolving cyclic or shared schema references without incurring linear lookup overhead
- Data access components manage dual-indexed in-memory mappings where schemas must be retrievable both by schema object reference and by distinct string identifiers
- Recursive schema compilation processes must track active reference resolution paths to prevent infinite recursion and clean up transient traversal states upon completion
- Discriminator-based union evaluation relies on pre-indexed lookup maps to dispatch variant types efficiently rather than evaluating predicates sequentially

## Problem Statement

Unmanaged or linear schema lookups during parsing, transformation, and validation cause performance degradation and introduce circular reference hazards when traversing recursive structures. Without synchronized in-memory registries that maintain bidirectional mapping between schema identities and identifiers alongside active resolution caches, components risk memory leaks, stale metadata, and uncoordinated state during reference lifecycle operations.

## Decision

1. MUST: Schema metadata access and reference resolution MUST route through dedicated in-memory registry instances that provide dual mapping by schema object identity and identifier strings.

## Policy Block

- MUST Schema metadata access and reference resolution MUST route through dedicated in-memory registry instances that provide dual mapping by schema object identity and identifier strings.

In scope:
- Internal schema registry modules and metadata storage components
- Schema transformation and JSON schema translation pipelines
- Discriminated union type dispatch and cached lookup mechanisms

Out of scope:
- Stateless primitive validation operations that do not require external references or metadata persistence
- External database and persistent storage access layers outside in-memory schema operations

## Rationale

- Evidence across schema translation and core registry files demonstrates consistent reliance on dual-map structures to support bidirectional lookups between object references and unique identifiers
- Transient traversal state tracking via processing maps with explicit deletion upon completion prevents circular reference recursion during complex schema compilation
- Pre-indexing discriminator options and schema references eliminates repeated linear array searches across definition checks, reducing lookup complexity from linear to constant time

## Consequences

Positive:
- Provides deterministic constant-time retrieval of schema definitions and metadata by object identity or identifier
- Prevents infinite loops and stack overflow errors during recursive schema expansion through active path tracking
- Guarantees state synchronization between identity-based and identifier-based registries through coupled mutation primitives

Negative:
- Increases in-memory footprint due to duplicate references held within paired map structures
- Requires diligent cleanup and explicit deletion calls during traversal unwinding to avoid memory retention

## Alternatives

- Linear search across schema definition arrays and checks without dedicated index maps (rejected)
  Rejected because: Incurs linear time complexity on every lookup and fails to provide reliable circular reference detection across deep schema hierarchies
  When valid: Small schema structures with minimal properties where memory overhead of map indexing outweighs search time
- Attaching metadata and reference pointers directly as mutable properties on schema objects (rejected)
  Rejected because: Pollutes schema object structures, risks prototype pollution, and breaks object immutability guarantees across boundaries
  When valid: Private internal data representations where schema objects are disposable and not exposed to external callers

## Risks

- Failure to delete resolved entries from active processing maps could leak memory and falsely block subsequent traversals of the same reference path
  Mitigation: Wrap recursive resolution logic in structured try-finally blocks ensuring deletion executes upon traversal completion
  Owner: engineering team
- Partial deletions that remove entries from the primary map without clearing the corresponding identifier map cause inconsistent registry state
  Mitigation: Encapsulate deletion operations inside atomic registry methods that purge both indices simultaneously
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
- Ensure all reference caching layers utilize structured key serialization to avoid ambiguous reference path collisions across disparate namespaces
- Implement defensive cleanup in traversal contexts using finalizer blocks to guarantee deletion of transient processing tokens

## Continuation Context


Verify commands:
- # Discover and run the repository test command covering registry and reference caching modules
- # Discover and execute workspace type checking and linting scripts to verify data access boundaries

Accept when:
- All unit and integration test suites validating schema registry lookups, dual-map mutations, and reference cache resolution pass with zero errors
- Static type analysis confirms correct parameter and return types for all map access, mutation, and deletion calls without type coercion warnings

## Enforcement

- Verified by: Automated continuous integration pipeline executing repository test and lint scripts
- Verified by: Peer code review verifying synchronized dual-map mutations and structured traversal cleanup
- Violation handling: Pull requests containing uncoordinated map mutations, unindexed linear searches, or unmanaged reference loops are blocked from merging until corrected
- Exception process: Exceptions require written justification submitted to the architecture review team documenting why an isolated linear search or alternative caching strategy is necessary