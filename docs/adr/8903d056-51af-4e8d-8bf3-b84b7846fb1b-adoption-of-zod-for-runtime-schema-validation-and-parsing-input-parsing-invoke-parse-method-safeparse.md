---
version: 2
name: 8903d056-51af-4e8d-8bf3-b84b7846fb1b-adoption-of-zod-for-runtime-schema-validation-and-parsing-input-parsing-invoke-parse-method-safeparse
description: "Adoption of zod for Runtime Schema Validation and Parsing: Input Parsing Invoke Parse Method Safeparse"
metadata:
  actual:
    adr_id: 8903d056-51af-4e8d-8bf3-b84b7846fb1b
    status: accepted
    candidate_group_id: 3e4f306d-7388-4290-bc8e-3639ded660c1
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of zod for Runtime Schema Validation and Parsing: Input Parsing Invoke Parse Method Safeparse

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/resolution`

Applies to:
- `src/**`

## Context

- Runtime boundaries and module resolution endpoints require strict input validation to prevent invalid data ingestion.
- Static type checking does not guarantee runtime payload integrity across serialized boundaries or external invocation.
- The codebase requires a unified schema validation mechanism across all module formats and entrypoints.

## Problem Statement

Unvalidated input data passing into resolution logic introduces runtime failure risks and contract divergence across module interfaces. A standardized runtime validation approach is required to guarantee schema conformance upon ingestion.

## Decision

1. MUST: Input parsing MUST invoke the parse method or safeParse method on defined schemas rather than performing ad-hoc manual type assertions.

## Policy Block

- MUST Input parsing MUST invoke the parse method or safeParse method on defined schemas rather than performing ad-hoc manual type assertions.

In scope:
- Runtime input parsing and validation within module resolution entrypoints
- Data contracts interfacing with external inputs across module formats

Out of scope:
- Internal pure functions operating on already validated and typed structures
- Compile-time-only type declarations where runtime validation is not applicable

## Rationale

- zod provides composable schema definition with automatic type inference, ensuring that runtime validation logic and static type declarations remain aligned.
- Validating inputs via schema parsing prevents malformed payloads from propagating deeper into application logic.
- Consistent schema parsing across module entrypoints guarantees uniform runtime safety regardless of consumer module system.

## Consequences

Positive:
- Runtime payload integrity is guaranteed upon ingestion at module boundaries.
- Static types are inferred directly from schema definitions, eliminating contract divergence.
- Validation failures produce structured error information rather than unexpected runtime exceptions.

Negative:
- Schema execution introduces runtime overhead during input parsing.
- An external runtime dependency footprint is incurred across distributed module entrypoints.

## Alternatives

- Manual conditional type checking and assertions (rejected)
  Rejected because: Manual assertions are error-prone, verbose, difficult to maintain, and fail to provide unified static type inference.
  When valid: Valid only in minimal runtime environments with strict zero-dependency constraints.
- Compile-time type checking without runtime parsing (rejected)
  Rejected because: Static types are erased during compilation and cannot validate dynamic or serialized inputs at runtime.
  When valid: Valid when inputs are strictly guaranteed to originate from verified internal callers.

## Risks

- Validation parsing throwing uncaught exceptions on malformed input
  Mitigation: Handle parse errors at boundaries or adopt safeParse to capture structured failure results
  Owner: engineering team
- Schema definitions diverging from evolving downstream contract requirements
  Mitigation: Derive all downstream contract types directly from schema definitions
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
- Construct reusable schema objects for shared boundary primitives to prevent redundant declarations.
- Infer static types directly from schema definitions to maintain synchronization between compile-time and runtime models.

## Continuation Context


Verify commands:
- Discover the project verification script from the repository manifest and execute validation suites.
- Discover and run the project test execution command to verify schema parsing tests pass across all module entrypoints.

Accept when:
- All boundary inputs are validated via schema parsing without manual type casting.
- Verification suites pass with schema validation tests confirming rejection of invalid inputs and acceptance of valid inputs.

## Enforcement

- Verified by: Continuous integration test execution
- Verified by: Automated code review and lint checks
- Verified by: Peer review of pull requests touching boundary entrypoints
- Violation handling: Pull requests bypassing schema validation on external inputs are blocked from merging.
- Violation handling: Code review flags any unvalidated boundary type assertions for refactoring.
- Exception process: Exceptions require documented justification demonstrating performance-critical constraints and approval by lead architects.