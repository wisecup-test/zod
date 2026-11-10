---
version: 2
name: eecf273f-964e-4f49-bfef-7b4d77923ab3-zod-schema-based-string-input-validation-before-implementing-validation-logic-third-party
description: "Zod Schema-Based String Input Validation: Before Implementing Validation Logic Third Party"
metadata:
  actual:
    adr_id: eecf273f-964e-4f49-bfef-7b4d77923ab3
    status: accepted
    candidate_group_id: 054bbc9c-809f-42bc-8a1f-4ab536b9134b
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Zod Schema-Based String Input Validation: Before Implementing Validation Logic Third Party

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/resolution`

Applies to:
- `src/**`

## Context

- Input validation is required at application boundaries to sanitize external inputs and prevent injection attacks or invalid state propagation.
- Static analysis detected multiple instances of Zod schema definitions performing synchronous string parsing on incoming values within a single resolution module.
- The pattern is isolated to a single file, indicating a local verification fixture or evaluation rather than a broadly adopted repository-wide architectural convention.

## Problem Statement

Unvalidated input strings entering internal domain modules risk propagating malformed data and exposing security vulnerabilities. A standardized mechanism is needed to enforce strict schema validation on string inputs before processing, while establishing whether runtime schema parsing should be adopted across the repository.

## Decision

1. MUST: Before implementing validation logic with a third-party schema library, the consumer MUST inspect the repository lock artifact to verify the exact resolved version and adhere to its published API specification.

## Policy Block

- MUST Before implementing validation logic with a third-party schema library, the consumer MUST inspect the repository lock artifact to verify the exact resolved version and adhere to its published API specification.

In scope:
- Boundary handlers, resolution modules, and services receiving external or untrusted string inputs.

Out of scope:
- Internal trusted subroutines where data has already been validated against formal schemas.

## Rationale

- Schema-driven parsing ensures runtime data adheres strictly to expected structural constraints, preventing security defects caused by unexpected inputs.
- Centralizing validation logic into declarative schema objects avoids duplicate manual type-checking routines across application layers.
- Evidence indicates localized usage of Zod string parsing, justifying evaluation of schema validation while acknowledging lack of multi-module architectural adoption.

## Consequences

Positive:
- Guarantees runtime structural validity of string inputs before domain execution.
- Reduces vulnerability surface area by blocking malformed or unexpected input payloads.
- Provides explicit error diagnostics when inputs fail schema constraints.

Negative:
- Incurs parsing latency and memory allocation overhead on each validation invocation.
- Synchronous parse exceptions require structured error handling to prevent unhandled process interruptions.

## Alternatives

- Manual string validation predicates and type guards (rejected)
  Rejected because: Manual type guards require extensive custom validation logic that is prone to implementation defects and drifts from domain specifications.
  When valid: Valid when external library dependencies cannot be introduced or in minimal standalone utility scripts.
- Safe parsing result objects instead of exception-throwing parse calls (deferred)
  Rejected because: Deferred pending repository-wide consensus on result-object return conventions versus exception-handling patterns.
  When valid: Valid in high-throughput hot paths where throwing exceptions introduces unacceptable runtime overhead.

## Risks

- Synchronous parse failures throwing uncaught exceptions causing unhandled request crashes.
  Mitigation: Encapsulate parse calls within structured error handling or adopt non-throwing parse equivalents at entry boundaries.
  Owner: Engineering Team
- Performance degradation in critical paths due to repeated schema instantiation and validation.
  Mitigation: Instantiate schemas as reusable module-level singletons rather than re-creating them inside function invocations.
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
- Define reusable schema objects at module scope rather than re-creating schemas inside request handlers.
- Coordinate schema validation with boundary error mappers to format parsing rejections into standardized error responses.

## Continuation Context


Verify commands:
- Discover and run the project test suite to verify that schema validation tests pass.
- Discover and run the project type checking and linting tasks to ensure type safety and rule compliance.

Accept when:
- All test suites asserting schema parsing behavior pass with zero failures.
- Static analysis and type checking pass without errors or type assertion bypasses.

## Enforcement

- Verified by: Continuous integration test pipelines and automated static analysis.
- Verified by: Peer code reviews on pull requests modifying boundary input handling.
- Violation handling: Pull requests lacking required boundary schema validation are blocked from merging until compliant schemas are introduced.
- Exception process: Exceptions require approval from the security architecture lead with documented rationale demonstrating equivalent boundary sanitization.