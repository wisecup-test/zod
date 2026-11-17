---
version: 2
name: cd0cb892-307f-40f2-84d3-986246bb775e-standard-runtime-console-error-logging-developers-output-diagnostic-error-events-through
description: "Standard Runtime Console Error Logging: Developers Output Diagnostic Error Events Through"
metadata:
  actual:
    adr_id: cd0cb892-307f-40f2-84d3-986246bb775e
    status: accepted
    candidate_group_id: 0318f53e-f66b-41c4-b5c6-a73f38d34e4f
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
      - loaders/**
---

# Standard Runtime Console Error Logging: Developers Output Diagnostic Error Events Through

Status: proposed
Date: 2025-05-15
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `components/**`
- `loaders/**`

## Context

- Runtime execution errors and unexpected asynchronous failures must be recorded for diagnostic purposes.
- Both server-side data loading pipelines and client-side user interaction components capture and report failure conditions.
- Existing implementations output diagnostic messages directly through standard runtime console facilities without third-party logging dependencies.

## Problem Statement

Uncaught exceptions and operational errors require visibility without introducing complex external logging dependencies into lightweight client and loader modules.

## Decision

1. MUST: Developers MUST output diagnostic error events through runtime console error methods when no dedicated logging service is configured for the module scope.

## Policy Block

- MUST Developers MUST output diagnostic error events through runtime console error methods when no dedicated logging service is configured for the module scope.

In scope:
- All asynchronous error handlers and boundary catch blocks in client and server runtime scopes lacking dedicated telemetry services.

Out of scope:
- Modules that integrate dedicated telemetry clients, analytics reporters, or structured audit trails.

## Rationale

- Evidence demonstrates consistent use of standard runtime console error methods across distinct application layers.
- Using built-in console facilities avoids bundle size inflation and avoids external operational dependencies.

## Consequences

Positive:
- Zero dependency footprint and zero configuration overhead for recording runtime failures.
- Universal compatibility across both client-side and server-side execution contexts.

Negative:
- Logs lack uniform structured metadata required for centralized aggregation and searching.
- Log formatting and severity level handling remain uncoordinated across runtime environments.

## Alternatives

- Structured centralized logging framework adoption (rejected)
  Rejected because: The analyzed codebase relies exclusively on standard runtime console facilities rather than adopting an external logging framework.
  When valid: When distributed tracing, log aggregation services, or structured output formats are required.

## Risks

- Potential exposure of sensitive information through unstructured log output.
  Mitigation: Ensure error message formatting avoids logging sensitive runtime environment variables or credentials.
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
- Inspect repository dependency configurations to verify whether structured logging frameworks are introduced before adding ad-hoc console statements.
- Ensure error diagnostic outputs provide descriptive action context and capture original exception objects without leaking sensitive credentials.

## Continuation Context


Verify commands:
- Discover and execute the project verification scripts through the repository build system to check for code analysis and linting compliance.
- Run repository test suites to ensure error handling paths and diagnostic outputs function without unhandled promise rejections.

Accept when:
- Automated static analysis verification passes without reporting unhandled exception suppressions.
- Error dispatch sites conform to contextual messaging guidelines across all target modules.

## Enforcement

- Verified by: Static analysis and code review checks confirming diagnostic messaging adheres to standard error reporting practices.
- Violation handling: Code review failure and pull request rejection for silent failure suppression or non-compliant error logging.
- Exception process: Submit an architectural change request proposing a centralized logging adoption when structured telemetry is required.