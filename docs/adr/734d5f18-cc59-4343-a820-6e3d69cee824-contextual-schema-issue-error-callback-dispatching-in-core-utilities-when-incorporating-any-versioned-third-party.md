---
version: 2
name: 734d5f18-cc59-4343-a820-6e3d69cee824-contextual-schema-issue-error-callback-dispatching-in-core-utilities-when-incorporating-any-versioned-third-party
description: "Contextual Schema Issue Error Callback Dispatching in Core Utilities: When Incorporating Any Versioned Third Party"
metadata:
  actual:
    adr_id: 734d5f18-cc59-4343-a820-6e3d69cee824
    status: accepted
    candidate_group_id: 1df335b8-ed46-4669-9a07-fb77737e330d
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Contextual Schema Issue Error Callback Dispatching in Core Utilities: When Incorporating Any Versioned Third Party

Status: proposed
Date: 2025-05-15
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/core/**`

## Context

- Schema validation utilities require a mechanism to report issues and operational errors without directly binding to a concrete logging framework.
- Observability hooks are embedded into schema definition structures and execution contexts to enable custom error emission.
- The observed codebase relies on contextual error callback hooks alongside reflection primitives within core utility functions.

## Problem Statement

Emitting telemetry and diagnostic error logs from within core schema validation utilities risks coupling the low-level library to concrete logging engines or polluting standard streams, requiring a lightweight callback mechanism to delegate error observation to contextual callers.

## Decision

1. MUST: When incorporating any versioned third-party dependency into the observability pipeline, consumers MUST verify the project lock artifact to resolve the exact dependency version prior to use.

## Policy Block

- MUST When incorporating any versioned third-party dependency into the observability pipeline, consumers MUST verify the project lock artifact to resolve the exact dependency version prior to use.

In scope:
- Core schema utility functions that process validation issues and error records.
- Validation context definitions and schema instance configurations supporting optional error listeners.

Out of scope:
- Application-level services managing operational log aggregation and external log transport.
- User-facing presentation components consuming formatted error messages.

## Rationale

- Contextual error callbacks allow caller-defined telemetry capture while keeping core schema utilities free from external logging dependencies.
- Optional invocation syntax ensures execution proceeds without runtime failure even when no observability handler is registered.

## Consequences

Positive:
- Decouples core schema utility evaluation from specific logging engines or external observability frameworks.
- Allows contextual issue inspection and custom error logging handlers to be attached per schema definition or validation invocation.

Negative:
- Invoking arbitrary consumer-provided callbacks inside core validation pathways can introduce unpredictable latency.
- Single-file utility scope limits the consistency of observability across broader subsystem components.

## Alternatives

- Global centralized logger singleton invocation inside utility routines (rejected)
  Rejected because: Couples low-level validation utilities to a specific logging framework and degrades portability across execution environments.
  When valid: Valid when operating within an application service boundary with an established global logger.
- Direct console output emission during schema issue creation (rejected)
  Rejected because: Produces uncontrollable side effects during schema evaluation and prevents consumers from intercepting or formatting error data.
  When valid: Valid only in isolated local prototyping environments.

## Risks

- Consumer-provided error callbacks may throw unhandled runtime errors during issue reporting.
  Mitigation: Wrap callback executions or use non-throwing invocation semantics to ensure logging exceptions do not crash validation pipelines.
  Owner: engineering team
- Consumer error handlers may attempt to mutate internal issue structures during observation.
  Mitigation: Enforce documentation on callback signatures and pass read-only issue structures to prevent unintended mutation.
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
- Implement error handlers to fail safely so that logging failures do not interrupt core schema evaluation.
- Ensure contextual error functions adhere to minimal interface contracts to avoid leaking internal validation structures.

## Continuation Context


Verify commands:
- Discover the project test runner from the repository manifest and execute all unit tests governing core schema utility error paths.
- Discover the static analysis tool from the repository configuration and verify compliance with optional callback invocation rules.

Accept when:
- All unit and regression test suites for core schema utilities pass with zero failures.
- Static analysis confirms that error callbacks are executed exclusively through guarded optional invocation patterns.

## Enforcement

- Verified by: Automated static analysis checks executed during continuous integration.
- Verified by: Peer code review of modifications to core validation and utility modules.
- Violation handling: Pull requests introducing unhandled console logging or hardcoded logging dependencies in core utilities will be blocked.
- Violation handling: Violating changes must be refactored to use contextual error callbacks or passed context handlers before merging.
- Exception process: Submit an architectural review request detailing why an alternative telemetry or logging mechanism is required for the affected module.
- Exception process: Secure documented approval from the library maintainers before bypassing contextual callback conventions.