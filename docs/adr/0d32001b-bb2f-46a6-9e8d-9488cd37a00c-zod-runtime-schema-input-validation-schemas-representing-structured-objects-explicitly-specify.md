---
version: 2
name: 0d32001b-bb2f-46a6-9e8d-9488cd37a00c-zod-runtime-schema-input-validation-schemas-representing-structured-objects-explicitly-specify
description: "Zod Runtime Schema Input Validation: Schemas Representing Structured Objects Explicitly Specify"
metadata:
  actual:
    adr_id: 0d32001b-bb2f-46a6-9e8d-9488cd37a00c
    status: accepted
    candidate_group_id: 0b9e35e4-1818-4c41-93b8-39ce7b8dced7
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
      - src/v4/**
---

# Zod Runtime Schema Input Validation: Schemas Representing Structured Objects Explicitly Specify

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v3/**`
- `src/v4/**`

## Context

- Boundary components ingest variable external data structures and dynamic representations that must be validated prior to processing.
- Static type assertions alone do not enforce data validity across external serialization boundaries at runtime.
- Inconsistent validation implementations create vulnerabilities to invalid inputs and unexpected runtime failures across transformation layers.

## Problem Statement

Ingesting unvalidated or weakly validated data across serialization boundaries risks runtime exceptions, data corruption, and security vulnerabilities from malformed input structures.

## Decision

1. SHOULD: Schemas representing structured objects SHOULD explicitly specify key shapes and nested type constraints rather than allowing unconstrained records.

## Policy Block

- SHOULD Schemas representing structured objects SHOULD explicitly specify key shapes and nested type constraints rather than allowing unconstrained records.

In scope:
- All external data ingestion boundaries, serialized payload parsers, and schema translation utilities.
- Components processing untrusted, dynamic, or externally supplied data structures.

Out of scope:
- Internal function calls operating entirely within trusted domain boundaries where inputs were validated upon entry.
- Isolated internal algorithms operating exclusively on validated immutable structures.

Exceptions:
- EXC-42-001: Extreme performance constraints where schema parsing overhead is demonstrably prohibitive on hot execution paths.

## Rationale

- Adopting Zod schemas for input validation provides declarative, composable runtime type checking with inferred static typing across boundary layers.
- The use of parse and safeParse across twelve components demonstrates an architectural standard for verifying external inputs and schema transformations prior to internal consumption.

## Consequences

Positive:
- Eliminates injection of malformed data into domain workflows by enforcing structural contracts at runtime boundaries.
- Guarantees alignment between runtime data validation and static compile-time type structures.
- Standardizes structured error reporting across data ingestion and transformation layers.

Negative:
- Runtime processing overhead incurred during schema evaluation and recursive structure parsing.
- Maintenance overhead of keeping schema definitions synchronized with external contract modifications.

## Alternatives

- Manual conditional type-checking and custom assertion functions (rejected)
  Rejected because: Manual validation lacks composability, increases human error, and fails to provide inferred type guarantees.
  When valid: Acceptable only in micro-benchmarks or zero-dependency kernel environments with minimal boundary surfaces.
- Unchecked runtime type assertions relying strictly on static type definitions (rejected)
  Rejected because: TypeScript types are erased at runtime and provide zero protection against untrusted or malformed runtime payloads.
  When valid: Valid only for internal trusted interfaces where data integrity has already been proven at an outer boundary.

## Risks

- Excessive runtime validation overhead on high-throughput data processing pathways.
  Mitigation: Benchmark schema execution on performance-critical paths and utilize memoized or optimized schema instances.
  Owner: Engineering Team
- Schema drift leading to rejection of legitimate payloads after external schema updates.
  Mitigation: Centralize shared schema definitions and ensure automated test suites validate schemas against contract updates.
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
- Construct modular schemas using primitive and composite definitions that closely reflect boundary payload requirements.
- Prefer safeParse over parse when validation failures are handled as standard non-exceptional control flows.

## Continuation Context


Verify commands:
- Discover and execute the project test runner to verify input validation test suites pass successfully.
- Discover and execute the static analysis script to verify schema definitions and usage across boundary modules.

Accept when:
- All boundary ingestion routines execute Zod schema validation without bypassing parse or safeParse checks.
- Automated test suites confirm malformed inputs are safely rejected before reaching internal business logic.

## Enforcement

- Verified by: Automated continuous integration checks executing repository test suites and contract validation tests.
- Verified by: Peer code reviews ensuring all newly introduced boundary endpoints parse inputs via Zod schemas.
- Violation handling: Pull requests containing unvalidated boundary inputs are blocked from merging until schema checks are added.
- Violation handling: Runtime unhandled input validation exceptions trigger immediate alerting and remediation tickets.
- Exception process: Architecture review board approval documented in an architectural exception record with explicit residual risk acceptance.
- Exception process: Demonstrated benchmark proof showing validation overhead exceeds allowable latency thresholds in critical paths.