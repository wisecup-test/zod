---
version: 2
name: 0b34aae9-0189-4389-829b-cd9886ebb7c5-zod-schema-based-runtime-input-validation-untrusted-data-entering-system-integration-persistence
description: "Zod Schema-Based Runtime Input Validation: Untrusted Data Entering System Integration Persistence"
metadata:
  actual:
    adr_id: 0b34aae9-0189-4389-829b-cd9886ebb7c5
    status: accepted
    candidate_group_id: 38b8990c-6d46-441e-b801-6e145df51cbc
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/ai-sdk/**
      - fixtures/drizzle-zod/**
      - fixtures/internal-types/**
---

# Zod Schema-Based Runtime Input Validation: Untrusted Data Entering System Integration Persistence

Status: proposed
Date: 2025-05-19
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/integration`

Applies to:
- `fixtures/ai-sdk/**`
- `fixtures/drizzle-zod/**`
- `fixtures/internal-types/**`

## Context

- External and integration boundaries receive untyped and potentially hostile data payloads that must be sanitized before processing.
- Type assertions alone do not survive runtime execution and cannot protect internal domain models from malformed input.
- The codebase adopts schema declaration patterns to enforce runtime contracts and infer static types across integration points.

## Problem Statement

External inputs and integration boundaries introduce untrusted data into the application. Without deterministic runtime validation, invalid, malformed, or malicious payloads can penetrate internal business logic and persistence layers, leading to runtime failures, type confusion, or security vulnerabilities.

## Decision

1. MUST: All untrusted data entering the system at integration, persistence, and external boundaries MUST be validated against declared zod schemas prior to consumption.

## Policy Block

- MUST All untrusted data entering the system at integration, persistence, and external boundaries MUST be validated against declared zod schemas prior to consumption.

In scope:
- All incoming network payloads, database integration schemas, AI model structured inputs, and untrusted boundary boundaries.

Out of scope:
- Internal trusted function invocations within verified module isolation boundaries.

Exceptions:
- EXC-42-001: High-throughput internal memory channels where inputs have already been verified at the entry boundary.

## Rationale

- Runtime schema validation using Zod ensures incoming payloads conform to structural, numeric, and string constraints before execution.
- Safe parsing interfaces allow graceful error reporting without triggering unhandled exceptions across application boundaries.
- Static type inference directly derived from runtime schemas eliminates divergence between runtime validation rules and compile-time contracts.

## Consequences

Positive:
- Guarantees strict runtime boundary validation and prevents injection or malformed data attacks.
- Unifies compile-time static types with runtime verification through automatic type inference.
- Standardizes error handling for invalid input structures across integration endpoints.

Negative:
- Adds runtime execution overhead for parsing and validating complex nested payload structures.
- Requires maintaining schema definitions alongside or as the source of truth for domain types.

## Alternatives

- Manual imperative boundary validation functions (rejected)
  Rejected because: Manual validation logic is error-prone, duplicates type definitions, and fails to guarantee synchronization between runtime checks and compile-time types.
  When valid: Valid only in ultra-constrained environments where zero external dependencies are permitted.
- Compile-time type assertions without runtime validation (rejected)
  Rejected because: Type assertions are erased at runtime and provide zero protection against malformed or hostile external payloads.
  When valid: Valid only for internal trusted function calls where data has already passed boundary validation.

## Risks

- Performance degradation from parsing large or deeply nested payloads on high-frequency paths.
  Mitigation: Apply benchmarked schema compilation and avoid redundant nested re-parsing on internal call paths.
  Owner: Engineering team
- Schema definitions diverging from domain model expectations over time.
  Mitigation: Derive domain types directly from schemas rather than maintaining separate interface declarations.
  Owner: Engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Construct schemas using modular combinators to enable reusability across data layers and integration adapters.
- Handle parsing results defensively by isolating error recovery at the boundary layer without leaking internal stack traces.

## Continuation Context


Verify commands:
- Discover the repository test runner from the project manifest and execute the schema validation test suite.
- Locate the repository typecheck and linter configurations from the build manifest to verify schema declarations compile without errors.

Accept when:
- All boundary input validation tests pass against declared schemas without unhandled runtime exceptions.
- Static type verification confirms that inferred output types align with declared schema definitions across integration boundaries.

## Enforcement

- Verified by: Automated verification suites executing boundary validation test cases.
- Verified by: Static analysis rules preventing unvalidated input ingestion at integration boundaries.
- Verified by: Peer review verification during code integration.
- Violation handling: Pull requests introducing unvalidated boundary inputs or unsanitized type casts are blocked.
- Violation handling: Runtime validation failures at system boundaries are logged and rejected with structured validation errors.
- Exception process: Submit an architectural exception request detailing why schema validation is infeasible at the given boundary.
- Exception process: Require explicit approval from the application security and architecture review teams before bypassing boundary schema parsing.