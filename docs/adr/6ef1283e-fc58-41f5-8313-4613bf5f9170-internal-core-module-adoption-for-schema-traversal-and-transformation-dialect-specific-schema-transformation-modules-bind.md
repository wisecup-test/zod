---
version: 2
name: 6ef1283e-fc58-41f5-8313-4613bf5f9170-internal-core-module-adoption-for-schema-traversal-and-transformation-dialect-specific-schema-transformation-modules-bind
description: "Internal Core Module Adoption for Schema Traversal and Transformation: Dialect Specific Schema Transformation Modules Bind"
metadata:
  actual:
    adr_id: 6ef1283e-fc58-41f5-8313-4613bf5f9170
    status: accepted
    candidate_group_id: 64424c11-2cbc-426e-8f54-ae38ba571b66
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Adoption for Schema Traversal and Transformation: Dialect Specific Schema Transformation Modules Bind

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/**`

## Context

- Multiple schema dialect implementations require structural traversal and transformation operations that share underlying algorithmic requirements.
- Re-implementing schema tree-walking and structural utilities within each dialect module leads to behavioral divergence and code duplication.
- An internal core module centralizes common visitor routines and utility functions while delegating schema-specific definitions to dialect modules.
- Dialect transformation modules depend on shared traversal and utility interfaces from the internal core module to ensure uniform schema manipulation.

## Problem Statement

Schema dialects require consistent deep traversal and transformation capabilities without duplicating complex recursive visitor logic across independent dialect implementations or tightly coupling distinct dialect schemas together.

## Decision

1. MUST: Dialect-specific schema transformation modules MUST bind traversal operations to local schema definitions while keeping traversal mechanics centralized in the internal core module.

## Policy Block

- MUST Dialect-specific schema transformation modules MUST bind traversal operations to local schema definitions while keeping traversal mechanics centralized in the internal core module.

In scope:
- Implementation of schema transformation, traversal, and utility operations across dialect modules.
- Internal module structures sharing common structural inspection and manipulation logic.

Out of scope:
- Self-contained schema definitions that do not perform recursive traversal or structural transformation.
- External boundary adapters that do not manipulate internal schema trees.

## Rationale

- Centralizing recursive visitor algorithms in an internal core module guarantees identical traversal semantics across all dialect variations.
- Separating shared traversal logic from dialect-specific schema definitions isolates dialect syntax differences from underlying structural mechanics.
- Reusing internal core utilities reduces maintenance overhead and minimizes the risk of inconsistent edge-case handling across dialect implementations.

## Consequences

Positive:
- Traversal logic and structural transformation algorithms are maintained in a single core location.
- Consistent schema walking behavior is guaranteed across distinct dialect implementations.
- Dialect modules remain focused on syntax and dialect-specific definitions without duplicating visitor machinery.

Negative:
- Dialect transformation modules depend directly on internal core module interfaces, requiring disciplined internal interface stability.
- Changes to core traversal mechanics risk impacting all consuming dialect modules simultaneously.

## Alternatives

- Implement independent schema traversal and transformation routines directly within each dialect module (rejected)
  Rejected because: Duplicating recursive visitor logic across dialects increases maintenance burden and leads to inconsistent schema traversal edge cases
  When valid: When dialect implementations share no structural commonality or require fundamentally divergent traversal algorithms
- Unify all dialect definitions and transformation logic into a single monolithic module without internal layering (rejected)
  Rejected because: Monolithic bundling prevents distinct dialect packaging and increases bundle size for consumers needing only a lightweight dialect
  When valid: When the library exposes only a single schema dialect with no alternative variants

## Risks

- Breaking changes in the internal core module visitor interface may disrupt all dependent dialect transformations
  Mitigation: Establish regression test suites verifying transformation behavior across all dialects when core visitor mechanics change
  Owner: engineering team
- Dialect-specific requirements may tempt developers to introduce dialect-aware logic into the shared core module
  Mitigation: Enforce unidirectional dependency boundaries through static analysis and architectural review
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
- Locate the internal core module traversal exports and utility interfaces before implementing new schema transformation capabilities.
- Verify that dialect-specific transformation functions delegate recursive structural inspection to the core visitor interface while providing dialect-appropriate replacement schemas.

## Continuation Context


Verify commands:
- Discover and run the project test suite from the repository manifest to verify schema transformation consistency across all dialect modules.
- Discover and execute the project static analysis and lint checks to confirm module dependency boundaries and verify that core modules do not depend on dialect submodules.

Accept when:
- All schema transformation and traversal tests pass across both full and lightweight dialect implementations.
- Module boundary analysis confirms unidirectional dependencies from dialect transformation modules to the internal core module.

## Enforcement

- Verified by: Continuous integration test validation verifying schema transformation correctness across all dialect modules.
- Verified by: Static analysis checks detecting disallowed circular dependencies between internal core modules and dialect modules.
- Verified by: Pull request architectural code reviews evaluating dependency imports and visitor usage.
- Violation handling: Pull requests duplicating traversal logic or introducing circular imports from core to dialect modules will be blocked at continuous integration.
- Violation handling: Violations discovered in review must be refactored to consume shared visitor and utility routines from the internal core module.
- Exception process: Exceptions require documented justification detailing why the internal core traversal interface cannot support the specific transformation requirement, approved by core maintainers.