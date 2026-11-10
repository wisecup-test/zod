---
version: 2
name: 5546a915-08c6-4e45-a566-459e09469354-zod-core-json-schema-transformation-modules-metadata-retrieval-schema-definitions-during-transformation
description: "Zod Core JSON Schema Transformation Modules: Metadata Retrieval Schema Definitions During Transformation"
metadata:
  actual:
    adr_id: 5546a915-08c6-4e45-a566-459e09469354
    status: accepted
    candidate_group_id: bf562f7e-2eba-4e98-a358-82c1dab13f6c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Zod Core JSON Schema Transformation Modules: Metadata Retrieval Schema Definitions During Transformation

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `packages/zod/src/v4/core/**`

## Context

- The core validation library requires translating runtime validation schemas into standard JSON Schema specifications.
- Complex schemas frequently contain circular references, recursive relationships, and rich metadata definitions that require structured traversal management.
- Direct monolithic generation approaches lead to tightly coupled code that is difficult to maintain and extend across diverse schema types.

## Problem Statement

Generating compliant JSON Schema from expressive, composable runtime validation schemas requires handling recursive references, metadata resolution, and diverse schema types without bloating core schema instances or creating unmaintainable monolithic conversion functions.

## Decision

1. MUST: Metadata retrieval for schema definitions during transformation MUST resolve through a dedicated metadata registry interface on the traversal context rather than direct schema inspection.

## Policy Block

- MUST Metadata retrieval for schema definitions during transformation MUST resolve through a dedicated metadata registry interface on the traversal context rather than direct schema inspection.

In scope:
- Core schema transformation and JSON Schema generation modules within the library.
- Context management, schema processor registries, and metadata lookup implementations.

Out of scope:
- Runtime data validation paths that do not generate JSON Schema representations.
- External schema format converters operating outside the core library module boundaries.

## Rationale

- Partitioning the translation pipeline into dedicated processors coordinated by a traversal context separates concerns between schema definition and serialization.
- Context-based seen caches reliably detect and resolve cyclic references during traversal.
- Registry abstraction standardizes metadata extraction across disparate schema varieties without contaminating schema definitions with serialization-specific properties.

## Consequences

Positive:
- Decouples individual schema transformation logic into discrete, independently testable processor units.
- Prevents infinite loops on recursive and self-referencing schemas through context-driven seen caching.
- Centralizes metadata extraction through registry lookups rather than scattered ad-hoc property access.

Negative:
- Increases architectural indirection by requiring all processors to coordinate through shared context abstractions.
- Requires new schema types to provide corresponding processor registrations to maintain complete JSON Schema parity.

## Alternatives

- Monolithic single-function schema serializer (rejected)
  Rejected because: A monolithic translation function creates high cognitive complexity, prevents isolated testing of individual schema representations, and complicates cyclic reference tracking.
  When valid: Valid only in small libraries supporting a minimal, non-recursive schema subset.
- Direct schema method polymorphism where each schema instance emits its own JSON Schema (rejected)
  Rejected because: Embedding serialization directly into schema definitions increases runtime bundle overhead and entangles core validation logic with target-specific serialization formats.
  When valid: Valid when schema definitions are exclusively used for serialization with no separate validation or metadata concerns.

## Risks

- Inconsistent context propagation across custom or third-party schema processors leading to untracked circular loops.
  Mitigation: Enforce strict traversal context passing via automated contract tests and shared transformation utilities.
  Owner: Core Architecture Team
- Cache collisions or incomplete cache invalidation across reused contexts.
  Mitigation: Instantiate isolated context objects per top-level transformation invocation.
  Owner: Core Architecture Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Implementers must ensure all schema traversal operations thread the context object uniformly across all processor dispatch calls.
- Cache mutations on the visited registry must occur prior to traversing nested child schemas to ensure cyclic graph definitions terminate cleanly.

## Continuation Context


Verify commands:
- Discover the repository configuration to locate and execute the test runner targeting core schema conversion modules.
- Discover the workspace static analysis and linting scripts to verify compliance with internal module dependency boundaries.

Accept when:
- The repository test suite executes without failures across all JSON Schema generation scenarios, including recursive and circular definitions.
- Static boundary checks confirm schema transformation processors only interact with core registries through the context interface.

## Enforcement

- Verified by: Automated unit and integration test suites validating schema-to-JSON-Schema conversions.
- Verified by: Static analysis and code review inspecting module import boundaries and context threading.
- Violation handling: Pull requests bypassing the traversal context or directly coupling schema definitions to serialization logic are rejected during code review.
- Exception process: Exceptions for specialized schema transformations must be submitted to the core architecture maintainers with technical justification demonstrating why context-based dispatch is infeasible.