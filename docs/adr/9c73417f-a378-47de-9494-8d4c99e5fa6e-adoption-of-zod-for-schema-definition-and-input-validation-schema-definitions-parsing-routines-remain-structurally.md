---
version: 2
name: 9c73417f-a378-47de-9494-8d4c99e5fa6e-adoption-of-zod-for-schema-definition-and-input-validation-schema-definitions-parsing-routines-remain-structurally
description: "Adoption of Zod for Schema Definition and Input Validation: Schema Definitions Parsing Routines Remain Structurally"
metadata:
  actual:
    adr_id: 9c73417f-a378-47de-9494-8d4c99e5fa6e
    status: accepted
    candidate_group_id: d82ab627-4321-406c-a644-2305a03bee19
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of Zod for Schema Definition and Input Validation: Schema Definitions Parsing Routines Remain Structurally

Status: proposed
Date: 2025-05-14
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/resolution`

Applies to:
- `src/**`

## Context

- Applications require runtime input validation to protect internal components from malformed or unexpected data structures.
- Static type checking does not validate data arriving at runtime boundaries, requiring a runtime schema enforcement library.
- The codebase requires consistent schema parsing across multiple module compilation formats.

## Problem Statement

Untrusted runtime inputs crossing module boundaries risk causing unpredictable runtime failures or corrupting application state if not validated against strict schemas. The architecture requires a unified, declarative validation mechanism that enforces data constraints and integrates across various module compilation targets.

## Decision

1. SHOULD: Schema definitions and parsing routines SHOULD remain structurally identical across all module compilation targets supported by the repository.

## Policy Block

- SHOULD Schema definitions and parsing routines SHOULD remain structurally identical across all module compilation targets supported by the repository.

In scope:
- All runtime input validation and payload parsing across module boundaries.
- Data ingestion points where external or untrusted structures must conform to defined schemas.

Out of scope:
- Internal compile-time type declarations that do not process external runtime inputs.
- Low-level primitive operations where data invariants are already established.

## Rationale

- Zod provides declarative schema definition coupled with automatic type inference, eliminating drift between compile-time types and runtime validation.
- Evidence demonstrates consistent application of Zod string schema parsing across different module targets, establishing uniform validation behavior.
- Centralizing on Zod ensures consistent error reporting and deterministic validation behavior across the codebase.

## Consequences

Positive:
- Runtime type safety and input integrity are enforced consistently at all module boundaries.
- Reduced boilerplate for input validation and schema definition through composable schema builders.
- Consistent validation error handling across different module compilation formats.

Negative:
- Introduces an external dependency and runtime overhead for schema evaluation.
- Creates direct coupling to the Zod API surface across module validation boundaries.

## Alternatives

- Manual custom validation routines without a schema library (rejected)
  Rejected because: Manual validation requires substantial boilerplate, lacks automatic type inference, and increases maintenance overhead.
  When valid: In resource-constrained environments where external dependencies cannot be introduced.
- Alternative schema validation libraries (rejected)
  Rejected because: Zod is already integrated across multiple module targets, and introducing an additional validation library would create fragmentation.
  When valid: When specific high-throughput serialization protocols require alternative schema engines.

## Risks

- Performance overhead from executing complex schema validation on high-frequency code paths.
  Mitigation: Design schemas efficiently and apply validation primarily at boundary ingress points.
  Owner: Engineering Team
- Schema parsing throwing unhandled exceptions at runtime.
  Mitigation: Catch parsing exceptions at boundary layers or utilize safe parsing mechanisms to handle invalid inputs gracefully.
  Owner: Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Declare validation schemas modularly so that schema definitions and parsing operations remain consistent across all module compilation formats.
- Handle validation failures at boundaries by catching parsing errors and transforming them into structured domain errors.

## Continuation Context


Verify commands:
- Discover the project's verification and test scripts from the repository manifest and execute them.
- Execute the repository test suite to confirm that schema validation runs without errors across all module formats.

Accept when:
- All schema validation parsing logic executes successfully across all supported module targets.
- Repository verification scripts complete with zero exit codes and no schema parsing errors.

## Enforcement

- Verified by: Continuous integration pipelines executing automated test suites.
- Verified by: Peer code review verifying that boundary inputs pass through Zod schema validation.
- Violation handling: Pull requests bypassing schema parsing for boundary inputs will be blocked during review.
- Violation handling: Test failures resulting from unhandled schema validation errors will block deployment.
- Exception process: Exceptions must be submitted via architectural review with documented rationale for bypassing schema validation.