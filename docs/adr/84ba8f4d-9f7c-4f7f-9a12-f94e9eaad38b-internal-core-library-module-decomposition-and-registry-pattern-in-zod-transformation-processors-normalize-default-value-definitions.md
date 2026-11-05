---
version: 2
name: 84ba8f4d-9f7c-4f7f-9a12-f94e9eaad38b-internal-core-library-module-decomposition-and-registry-pattern-in-zod-transformation-processors-normalize-default-value-definitions
description: "Internal Core Library Module Decomposition and Registry Pattern in Zod: Transformation Processors Normalize Default Value Definitions"
metadata:
  actual:
    adr_id: 84ba8f4d-9f7c-4f7f-9a12-f94e9eaad38b
    status: accepted
    candidate_group_id: fd8d8f66-6b2f-4c03-8911-bd9f1e5e7e6f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Internal Core Library Module Decomposition and Registry Pattern in Zod: Transformation Processors Normalize Default Value Definitions

Status: proposed
Date: 2025-05-15
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `packages/zod/src/v4/core/**`

## Context

- Core schema processing and transformation require coordinating distinct capabilities, including schema type definitions, validation checks, serialization logic, and metadata management.
- Recursive schema structures and self-referential definitions necessitate centralized cycle detection and reference resolution during schema transformation.
- Internal modularization is required to keep core validation components decoupled from specialized schema generation and serialization processors while preserving unified registry access.

## Problem Statement

Without a cohesive internal module decomposition and state-passing protocol, complex schema libraries risk monolithic codebase sprawl, tight coupling between core validation and serialization subsystems, and runtime failures caused by unhandled cyclic schema references.

## Decision

1. MAY: Transformation processors MAY normalize default value definitions and serialization artifacts through structured deep cloning mechanisms when immutability guarantees are required.

## Policy Block

- MAY Transformation processors MAY normalize default value definitions and serialization artifacts through structured deep cloning mechanisms when immutability guarantees are required.

In scope:
- All internal modules within the core library package responsible for schema definitions, validation checks, registry lookups, and schema transformations.
- Functions performing recursive schema graph analysis, serialization, or metadata aggregation.

Out of scope:
- Public-facing schema consumption code outside the internal core library package.
- Simple non-recursive utility functions that do not participate in schema transformation or metadata registration.

## Rationale

- Modularizing internal core components into dedicated submodules separates validation concerns from serialization processors, improving maintainability and testability.
- Employing a contextual traversal cache provides deterministic recursion guarding and reference deduplication for cyclic and self-referential schema graphs.
- Consolidating metadata management into explicit registries isolates instance tracking from schema instance definitions.

## Consequences

Positive:
- Decouples domain validation checks, schema representations, and serialization processors into focused, independently testable internal modules.
- Prevents stack overflow exceptions during recursive schema traversal by enforcing explicit cyclic structure tracking via contextual traversal caches.
- Provides centralized schema metadata indexing through dedicated registries without polluting core schema definition objects.

Negative:
- Internal submodules require disciplined adherence to dependency hierarchies to prevent circular initialization issues at module load time.
- Propagating contextual caching instances across all transformation steps increases call signature complexity across internal processing functions.
- Shared registry structures introduce state management requirements that must be carefully isolated across execution contexts.

## Alternatives

- Monolithic Core File Architecture (rejected)
  Rejected because: Consolidating all schema definitions, verification checks, registries, and serialization processors into a single file creates unmaintainable file sizes, inhibits modular tree-shaking, and complicates concurrent development.
  When valid: Viable only for minimal validation libraries with strictly bounded feature scopes and no recursive schema generation capabilities.
- Stateless Recursive Serialization without Shared Context (rejected)
  Rejected because: Traversing complex schema graphs without passing contextual visited caches causes infinite recursion on cyclic schema definitions and prevents consistent metadata propagation.
  When valid: Acceptable only when schema definitions are strictly guaranteed to be directed acyclic graphs.

## Risks

- Circular module dependencies between schema processors and core registries causing runtime initialization failures.
  Mitigation: Enforce unidirectional internal module import hierarchies and verify lack of circular references through automated linting and dependency tree analysis.
  Owner: engineering team
- Uncontrolled memory retention within contextual traversal caches during large batch schema processing.
  Mitigation: Scope traversal caches strictly to the lifecycle of individual transformation requests to prevent memory leakage across concurrent or repeated operations.
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
- Maintain clear layering between schema definition primitives, validation checks, and serialization processors to prevent circular module dependencies.
- Ensure the contextual traversal cache is initialized at the root of every recursive traversal and forwarded across all child processing operations.
- Keep global registries focused on instance lookup and metadata resolution rather than transient execution state.

## Continuation Context


Verify commands:
- Discover and execute the repository test runner to validate recursive schema generation, registry lookups, and serialization behaviors.
- Discover and execute the repository module boundary and circular dependency verification scripts to ensure import isolation between core submodules.
- Discover and execute the repository static type checker to verify internal interface compatibility across all core module boundaries.

Accept when:
- All core module interfaces and internal imports resolve through the defined module boundaries without circular module initialization errors.
- Schema transformations and serializations correctly track cyclic structures using the contextual traversal cache without memory leaks.
- Static type checking and automated regression suites pass completely across all core library components.

## Enforcement

- Verified by: Automated static analysis and module boundary linting executed during continuous integration.
- Verified by: Mandatory peer code review by core library maintainers focusing on internal import hierarchies and context propagation.
- Verified by: Comprehensive unit and integration test suites validating recursive schema transformation and cycle detection behavior.
- Violation handling: Pull requests containing direct circular module imports or bypassed registry context structures are blocked from merging.
- Violation handling: Code review rejections require refactoring non-compliant internal modules to align with designated module boundaries and context protocols.
- Exception process: Submit an architectural exception request detailing the structural constraints that preclude using standard internal core modules or registry context traversal.
- Exception process: Obtain formal approval from core library maintainers prior to merging any alternative state passing or module coupling pattern.