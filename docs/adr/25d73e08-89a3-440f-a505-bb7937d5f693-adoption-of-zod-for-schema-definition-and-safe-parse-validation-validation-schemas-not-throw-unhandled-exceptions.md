---
version: 2
name: 25d73e08-89a3-440f-a505-bb7937d5f693-adoption-of-zod-for-schema-definition-and-safe-parse-validation-validation-schemas-not-throw-unhandled-exceptions
description: "Adoption of Zod for Schema Definition and Safe Parse Validation: Validation Schemas Not Throw Unhandled Exceptions"
metadata:
  actual:
    adr_id: 25d73e08-89a3-440f-a505-bb7937d5f693
    status: accepted
    candidate_group_id: b4f55bd5-a322-4c04-b31c-7702542d2a0c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - play.ts
      - scripts/**
---

# Adoption of Zod for Schema Definition and Safe Parse Validation: Validation Schemas Not Throw Unhandled Exceptions

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `play.ts`
- `scripts/**`

## Context

- Runtime boundaries and operational scripts ingest dynamic external inputs that require structural verification.
- Uncaught exceptions thrown during data validation introduce unpredictable failures across execution workflows.
- Adopting a unified schema validation library establishes consistent type narrowing and validation logic across the codebase.

## Problem Statement

Modules and scripts handling dynamic inputs require reliable runtime validation without triggering unhandled exceptions or relying solely on static type assertions that evaporate at runtime. Without a standardized schema definition and parsing convention, divergent validation logic leads to inconsistent error representations and fragile execution boundaries.

## Decision

1. MUST_NOT: Validation schemas MUST NOT throw unhandled exceptions across module boundaries during runtime data parsing.

## Policy Block

- MUST_NOT Validation schemas MUST NOT throw unhandled exceptions across module boundaries during runtime data parsing.

In scope:
- Runtime data validation across scripts and operational entry points
- Schema definition and input boundary verification for untrusted data payloads

Out of scope:
- Internal function calls where static compile-time type guarantees are fully preserved
- Performance-critical inner loops where external schema validation overhead is demonstrably prohibitive

Exceptions:
- EXC-20-001: Low-level serialization routines require specialized binary decoders with pre-verified memory structures

## Rationale

- Using Zod safeParse produces predictable result objects containing either parsed data or structured issue lists, avoiding exception-driven control flow.
- Schema composition via primitive and object definitions aligns runtime validation contracts with static interface types.
- Standardizing on non-throwing validation simplifies error propagation and fuzzing inspection across test and runtime environments.

## Consequences

Positive:
- Eliminates unhandled exceptions during data parsing by standardizing on safeParse result objects.
- Enforces uniform runtime type narrowing and structural schema composition across components.
- Provides structured validation failure diagnostics without interrupting process execution.

Negative:
- Incurs runtime overhead associated with schema parsing and validation result object allocations.
- Requires calling code to inspect result discriminators before accessing validated properties.

## Alternatives

- Manual conditional validation checks and custom type predicates (rejected)
  Rejected because: Manual property validation is error-prone, verbose, and difficult to maintain across complex nested data structures
  When valid: Trivial scalar checks with no nested structures or external schema requirements
- Throwing parse operations enclosed in try-catch blocks (rejected)
  Rejected because: Exception-driven control flow introduces performance overhead and obscures predictable boundary error handling
  When valid: Top-level script initialization where any validation failure must immediately abort process execution

## Risks

- Engineers might attempt to access data properties without inspecting the validation success status
  Mitigation: Enforce strict property access after safeParse status checks through linting and code review
  Owner: engineering team
- Schema drift between runtime definitions and external payload contracts
  Mitigation: Maintain automated test suites that validate schemas against expected valid and invalid boundary payloads
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
- Construct schemas using primitive and composite definitions and validate incoming payloads with safeParse.
- Branch conditionally on the success property of the safeParse result object before accessing parsed values.

## Continuation Context


Verify commands:
- Discover the repository test runner from project configuration and execute the schema validation test suite.
- Run the project static analysis and linting scripts to verify compliance with non-throwing validation patterns.

Accept when:
- All schema validation tests execute and pass with zero unhandled exceptions.
- Input validation call sites use safeParse and handle validation failure cases explicitly.

## Enforcement

- Verified by: Automated continuous integration checks executing repository test suites
- Verified by: Peer code reviews verifying schema definitions and safeParse usage
- Violation handling: Pull requests introducing throwing parse methods or unvalidated inputs are rejected during code review.
- Violation handling: Existing non-compliant validation call sites must be refactored before merging.
- Exception process: Submit an architectural exception request detailing why standard schema validation is inapplicable.
- Exception process: Obtain approval from the technical lead and document the boundary isolation in module documentation.