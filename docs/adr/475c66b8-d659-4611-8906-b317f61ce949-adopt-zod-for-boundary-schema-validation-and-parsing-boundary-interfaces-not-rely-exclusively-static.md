---
version: 2
name: 475c66b8-d659-4611-8906-b317f61ce949-adopt-zod-for-boundary-schema-validation-and-parsing-boundary-interfaces-not-rely-exclusively-static
description: "Adopt Zod for Boundary Schema Validation and Parsing: Boundary Interfaces Not Rely Exclusively Static"
metadata:
  actual:
    adr_id: 475c66b8-d659-4611-8906-b317f61ce949
    status: accepted
    candidate_group_id: fbb66e81-14fa-4010-b455-96af3f3a2042
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adopt Zod for Boundary Schema Validation and Parsing: Boundary Interfaces Not Rely Exclusively Static

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/resolution`

Applies to:
- `src/**`

## Context

- Module entry points and package boundaries receive external data that must be validated prior to execution.
- Static type declarations alone cannot guarantee data integrity at runtime boundaries.
- The codebase requires a consistent schema declaration and parsing mechanism across all module resolution targets.

## Problem Statement

Data entering module boundaries and resolution entry points risks introducing runtime failures and security vulnerabilities if processed without strict schema validation and type parsing.

## Decision

1. MUST_NOT: Boundary interfaces MUST_NOT rely exclusively on static type assertions without runtime schema parsing.

## Policy Block

- MUST_NOT Boundary interfaces MUST_NOT rely exclusively on static type assertions without runtime schema parsing.

In scope:
- All public module interfaces and resolution entry points accepting external input data.
- Boundary parsing routines that process untrusted or polymorphic payloads.

Out of scope:
- Internal private helper functions where input arguments have already undergone boundary schema validation.
- Performance-critical low-level primitives where benchmarking demonstrates validation overhead is prohibitive.

## Rationale

- Evidence across module entry targets reveals consistent adoption of Zod string schema declarations and parse execution for input validation.
- Adopting a unified schema validation library standardizes input boundary enforcement across multiple module resolution formats.
- Declarative schema parsing reduces boilerplate validation logic and prevents unvalidated data from propagating into internal systems.

## Consequences

Positive:
- Enforces deterministic runtime data validation at module entry points.
- Aligns runtime validation behavior with static type inference.
- Provides structured parsing and centralized error reporting for invalid input data.

Negative:
- Introduces third-party dependency coupling for schema definitions at module entry points.
- Adds CPU parsing overhead during input validation on high-frequency execution paths.

## Alternatives

- Manual conditional type guards and imperative validation functions (rejected)
  Rejected because: Imperative checks increase code verbosity, introduce human error in boundary coverage, and fail to generate composable static types alongside runtime validation.
  When valid: Valid only in constrained environments where zero third-party dependencies are permissible and data shapes are trivial.
- Compile-time static type assertions without runtime validation (rejected)
  Rejected because: Static type assertions are erased at runtime and provide zero protection against malformed external data entering at module boundaries.
  When valid: Valid for internal function boundaries where input data has already been validated at the system boundary.

## Risks

- Runtime parsing overhead could degrade throughput on performance-critical execution paths.
  Mitigation: Reuse declared schema instances and isolate validation checks to system entry boundaries rather than re-evaluating inside internal loops.
  Owner: engineering team
- Breaking API changes between schema library versions could disrupt validation behavior.
  Mitigation: Enforce the Discovery Policy to lock the exact resolved version and maintain automated boundary test coverage across module targets.
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
- Define schemas alongside boundary interfaces and invoke schema parse operations at all entry points accepting external payloads.
- Handle validation parse exceptions at the boundary layer to ensure structured error messages are returned to callers.

## Continuation Context


Verify commands:
- Discover and run the repository verification scripts to verify that all schema parse invocations execute successfully against test inputs.
- Execute the project test suite to verify that boundary validation logic correctly parses valid data and rejects invalid inputs.

Accept when:
- All input parsing invocations execute through defined validation schemas without unhandled validation failures on valid inputs.
- The project test suite passes with full verification of boundary inputs against declared schema specifications.

## Enforcement

- Verified by: Automated test suite execution verifying input validation behavior across module boundaries.
- Verified by: Static analysis and peer code review of export definitions and boundary entry points.
- Violation handling: Pull requests with unvalidated boundary inputs or manual type assertions will be blocked until schema validation is introduced.
- Violation handling: Direct commits bypassing validation rules will trigger automated review failure.
- Exception process: Submit an architectural review request documenting technical constraints that preclude schema validation for specific low-level performance paths.
- Exception process: Obtain explicit sign-off from module maintainers before implementing custom parsing routines.