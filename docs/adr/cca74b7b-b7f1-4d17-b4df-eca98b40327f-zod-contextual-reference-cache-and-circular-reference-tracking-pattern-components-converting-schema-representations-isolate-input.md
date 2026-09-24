# Zod Contextual Reference Cache and Circular Reference Tracking Pattern: Components Converting Schema Representations Isolate Input

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Converting structural schema specifications into programmatic schema validator objects requires resolving nested and cyclic definitions across shared reference identifiers.
- Direct synchronous recursive descent over self-referencing schema pointers produces unbounded stack execution without explicit state tracking.
- The schema translation layer introduces a contextual cache and in-flight tracking set to memoize completed schema objects and isolate cyclic references during compilation.

## Problem Statement

Converting external schema definitions with cyclic or repeated reference identifiers leads to infinite recursion and redundant schema instantiation during runtime translation. Without centralized memoization and active traversal tracking, circular reference resolution fails, causing call stack overflows and duplicate validation model instances across the translation pipeline.

## Decision

1. SHOULD: Components converting schema representations SHOULD isolate input sanitization by parsing deep copies of source definitions prior to reference graph resolution.

## Policy Block

- SHOULD Components converting schema representations SHOULD isolate input sanitization by parsing deep copies of source definitions prior to reference graph resolution.

In scope:
- Translation of external schema specifications containing internal path references into programmatic validation schemas
- Resolution routines managing recursive or self-referential schema structures

Out of scope:
- Direct instantiation of validation schemas without cross-referential dependencies
- Stateless transformation pipelines with guaranteed directed acyclic structure

## Rationale

- Context-driven memoization via ctx.refs ensures that identical reference targets are parsed once and shared across validation trees, optimizing memory footprint.
- Tracking active traversals via ctx.processing detects circular reference cycles and prevents infinite call stack recursion during schema construction.
- Encapsulating cache and cycle state inside an ephemeral context structure avoids global mutable state while retaining deterministic resolution across recursive parsing boundaries.

## Consequences

Positive:
- Deterministic termination for cyclic and recursive schema graphs during compilation.
- Elimination of redundant schema object allocations through contextual memoization.
- Decoupled resolution lifecycle where state persists only for the duration of a single schema compilation process.

Negative:
- Introduces explicit coupling between compilation helper functions and the context state container.
- Memory consumption scales with the number of unique schema paths cached during translation.

## Alternatives

- Stateless inline reference expansion without cache (rejected)
  Rejected because: Causes unbounded recursion on cyclic schemas and duplicates schema instances on repeated references.
  When valid: Only valid for guaranteed non-recursive trees with strictly unique definitions.
- Global singleton registry for reference caching (rejected)
  Rejected because: Creates shared mutable state across independent schema translation calls, causing cross-request cache collisions and memory leaks.
  When valid: Valid in single-threaded environments with static, unchanging schemas loaded at bootstrap.

## Risks

- Failure to delete keys from the active processing set if compilation encounters an uncaught error leaves incomplete cycle state.
  Mitigation: Wrap reference compilation within structured resource release blocks ensuring cleanup of processing tracking entries.
  Owner: engineering team
- Cache collisions if distinct schema documents reuse identical local reference path identifiers in a shared context.
  Mitigation: Scope context instances strictly to individual translation invocations or partition cache namespaces by document root.
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
- Instantiate a fresh context object containing refs and processing collections at the entry point of each schema conversion routine.
- Ensure all downstream schema construction helpers accept and propagate the contextual reference cache.

## Continuation Context


Verify commands:
- Discover and run the project test runner to verify that recursive schema reference tests pass without stack overflow.
- Execute the project static analysis and linting suites to ensure context parameters are consistently passed to schema transformation calls.

Accept when:
- All unit tests covering circular and self-referencing schema compilation complete successfully without recursion errors.
- Static type analysis confirms all schema conversion functions conform to expected context signatures.

## Enforcement

- Verified by: Automated test suites executed during continuous integration validating cyclic schema translation.
- Verified by: Peer code review confirming proper usage of reference caching and cycle removal APIs.
- Violation handling: Pull requests omitting reference cache checks or cycle tracking cleanup in schema translation modules will be blocked during review.
- Violation handling: Static verification failures on context interface mismatches halt compilation.
- Exception process: Submit an architectural review request demonstrating that target schema definitions are strictly acyclic and non-reusable before bypassing contextual tracking.