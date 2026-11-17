---
version: 2
name: c323bc35-6476-4575-98de-a35b1258e254-console-logging-api-for-command-line-diagnostics-process-lifecycle-signal-handlers-ensure-termination
description: "Console Logging API for Command-Line Diagnostics: Process Lifecycle Signal Handlers Ensure Termination"
metadata:
  actual:
    adr_id: c323bc35-6476-4575-98de-a35b1258e254
    status: accepted
    candidate_group_id: 5ac8fa6c-ba70-4a06-a6bf-6c44c9428bc0
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Console Logging API for Command-Line Diagnostics: Process Lifecycle Signal Handlers Ensure Termination

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/tsc`

Applies to:
- `bench/**`

## Context

- Command-line benchmarking scripts require direct feedback mechanisms to inform users of invalid input arguments and runtime exit states.
- The codebase employs runtime console methods to emit diagnostic notices and process termination messages directly to standard streams.
- The detected usage is confined to an individual benchmarking script rather than an enterprise structured logging library.

## Problem Statement

Ad-hoc logging using native runtime output methods provides immediate terminal feedback for standalone scripts but lacks structured formatting, log level filtering, and centralized observability.

## Decision

1. MUST: Process lifecycle signal handlers MUST ensure termination status messages are written to the standard output stream prior to triggering process exit.

## Policy Block

- MUST Process lifecycle signal handlers MUST ensure termination status messages are written to the standard output stream prior to triggering process exit.

In scope:
- Command-line execution scripts and benchmarking harnesses requiring interactive terminal output.

Out of scope:
- Production server applications, core compiler transformation libraries, and services requiring structured telemetry aggregation.

## Rationale

- Direct runtime stream output via standard console methods satisfies lightweight script feedback requirements without introducing external dependency weight.
- Emitting parameter validation notices to standard error preserves the separation between operational diagnostics and programmatic standard output.
- Signal handling coupled with exit logging ensures explicit terminal confirmation during user-initiated interruptions.

## Consequences

Positive:
- Zero dependency footprint for standalone utility scripts.
- Immediate and unambiguous feedback delivered to interactive terminal sessions.
- Clear distinction between diagnostic failure messages on standard error and standard runtime output.

Negative:
- Absence of structured log metadata such as timestamps, correlation identifiers, and severity tags.
- Inability to aggregate or search log entries through centralized log analytics platforms.
- Risk of inconsistent log formats across multiple scripts if unstructured console calls proliferate.

## Alternatives

- Adopt an external structured logging library across all scripts and packages (rejected)
  Rejected because: Adding a third-party logging dependency to minimal benchmarking scripts introduces unnecessary build overhead and dependency surface area for simple CLI feedback.
  When valid: Valid when services emit high-volume logs to centralized ingestion backends requiring structured JSON formatting.
- Silent exit without terminal output during argument validation or interruption signals (rejected)
  Rejected because: Omitting user-facing error messages leaves terminal operators without actionable guidance on missing parameters or termination status.
  When valid: Valid when processes operate in headless, non-interactive batch pipelines where status codes alone convey failure.

## Risks

- Unstructured console logs may become difficult to parse if benchmarking outputs are consumed by automated pipelines.
  Mitigation: Ensure machine-readable benchmark results are written to discrete data files rather than interleaved with console diagnostic streams.
  Owner: engineering team
- Unmanaged console statements may proliferate into production libraries if not restricted to script boundaries.
  Mitigation: Enforce linting rules that prohibit console invocations within core packages while permitting them in standalone script directories.
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
- Standardize diagnostic output across command-line modules by wrapping runtime standard error output in a consistent utility interface when script complexity expands.
- Configure signal listeners to flush standard output streams prior to terminating runtime processes.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting verification scripts to check logging conventions across script boundaries.
- Discover and execute the repository test suite to ensure benchmarking scripts exit with expected status codes on invalid arguments.

Accept when:
- Static analysis validates that console output invocations are restricted to designated utility and script directories.
- Executing the benchmark script with missing arguments outputs an actionable error message to standard error and halts execution.

## Enforcement

- Verified by: Automated static analysis checks in continuous integration pipelines.
- Verified by: Peer review during pull requests affecting utility and benchmarking scripts.
- Violation handling: Pull requests containing unauthorized direct console invocations outside permitted script directories are blocked until resolved.
- Exception process: Exceptions for temporary debugging logs or alternative logging utilities must be documented in code comments and approved by module maintainers.