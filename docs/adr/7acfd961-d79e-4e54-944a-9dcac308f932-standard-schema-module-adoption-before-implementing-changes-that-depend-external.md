---
version: 2
name: 7acfd961-d79e-4e54-944a-9dcac308f932-standard-schema-module-adoption-before-implementing-changes-that-depend-external
description: "standard-schema Module Adoption: Before Implementing Changes That Depend External"
metadata:
  actual:
    adr_id: 7acfd961-d79e-4e54-944a-9dcac308f932
    status: accepted
    candidate_group_id: cde02561-665e-40aa-bc54-b52077956cb9
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# standard-schema Module Adoption: Before Implementing Changes That Depend External

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `packages/zod/src/v4/core/**`

## Context

- The validation core requires consistent schema representations across transformation pipelines and error dispatch mechanisms.
- Core submodules must interoperate without creating circular dependencies between schema transformation, error construction, and metadata registries.
- Adopting a standardized internal schema contract isolates cross-cutting transformation logic from vendor-specific engine internals.

## Problem Statement

Schema processing cores often suffer from tight coupling between internal error generation, AST representation, and serialization logic, leading to rigid architectures that cannot easily interoperate with broader schema standards.

## Decision

1. MUST: Before implementing changes that depend on external or shared specification packages, the consumer MUST discover the repository lock artifact and verify the exact resolved version and specification compliance.

## Policy Block

- MUST Before implementing changes that depend on external or shared specification packages, the consumer MUST discover the repository lock artifact and verify the exact resolved version and specification compliance.

In scope:
- All core schema transformation modules compiling or translating schemas across representation formats.
- All core error formatting and validation dispatch utilities requiring standardized schema contracts.

Out of scope:
- Platform-agnostic primitive helper functions that operate independently of schema contracts.
- User-facing convenience wrappers that consume already resolved schema instances.

## Rationale

- Static evidence reveals consistent dependence on standard-schema interfaces across both error processing and schema transformation modules.
- Centralizing standard schema definitions prevents contract drift between schema validation output and schema serialization pipelines.
- Decoupled contracts allow schema traversal logic to cleanly leverage metadata registries and traversal memoization without circular dependencies.

## Consequences

Positive:
- Decouples core error reporting and schema serialization from proprietary internal AST formats.
- Ensures schema transformation mechanisms adhere to consistent standard schema protocols.
- Facilitates centralized caching and metadata lookup integration across modular transformations.

Negative:
- Requires consistent maintenance of standard-schema adapter boundaries alongside internal engine representations.
- Introduces an indirection layer that must be reconciled during performance-critical schema traversals.

## Alternatives

- Directly coupled proprietary schema contracts across core modules (rejected)
  Rejected because: Coupling error generation and schema translation directly to proprietary schema representations prevents unified ecosystem interoperability and duplicates contract logic.
  When valid: Only acceptable in throwaway proof-of-concept prototypes that do not integrate with ecosystem tools.
- Ad-hoc inline interface definitions per module (rejected)
  Rejected because: Defining duplicate interfaces across transformation and error handling modules causes drift and breaks specification compliance.
  When valid: Acceptable in isolated external plugins with zero dependency sharing.

## Risks

- Evolving standard schema specifications may introduce contract drift if internal implementations lag behind.
  Mitigation: Maintain automated compliance tests against the canonical standard schema specification.
  Owner: engineering team
- Indirection layers could introduce minor performance overhead during deep recursive schema traversals.
  Mitigation: Benchmark schema conversion pipelines and utilize context-level seen-caches during traversal.
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
- Core schema modules should consume transformation cache contexts and metadata registries uniformly when resolving schema identities.
- Error handling modules must derive standard issue structures through standard-schema abstractions to preserve cross-system compatibility.

## Continuation Context


Verify commands:
- Discover the repository build and test script in the project manifest and execute the core test suite to verify contract compliance.
- Discover the repository linter and type-checker commands from project configuration and verify zero contract violations across core modules.

Accept when:
- All core schema transformations and error definitions pass automated type-checking and unit test suites verifying conformity to the standard-schema module contracts.
- Dependency analysis confirms no cyclic dependencies or direct bypasses of the standard-schema module in core schema transformation modules.

## Enforcement

- Verified by: Automated static analysis checks enforcing module import boundaries and contract adherence.
- Verified by: Pull request architecture review validating separation of core module dependencies.
- Violation handling: Pull request builds fail if circular imports or standard-schema contract bypasses are introduced.
- Violation handling: Violations must be refactored to consume the centralized standard-schema module before merging.
- Exception process: Architectural exceptions require submitting a formal RFC justifying why standard-schema contracts cannot represent the necessary capability.
- Exception process: Exceptions must define isolated boundaries that do not leak proprietary signatures into standard transformation pipelines.