---
version: 2
name: cfdbef7d-ff26-4ede-914e-7eed0a51e2f9-console-api-error-and-warning-stream-logging-in-operational-scripts-engineers-introducing-updating-script-dependencies-inspect
description: "Console API Error and Warning Stream Logging in Operational Scripts: Engineers Introducing Updating Script Dependencies Inspect"
metadata:
  actual:
    adr_id: cfdbef7d-ff26-4ede-914e-7eed0a51e2f9
    status: accepted
    candidate_group_id: 109ad59f-7122-451e-aab9-f1b755fbbae5
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - .claude/skills/triage/scripts/**
      - scripts/**
---

# Console API Error and Warning Stream Logging in Operational Scripts: Engineers Introducing Updating Script Dependencies Inspect

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `.claude/skills/triage/scripts/**`
- `scripts/**`

## Context

- Maintenance, integrity verification, and operational indexing scripts require immediate mechanisms to notify operators of execution failures, rule violations, and state discrepancies.
- Script executions run in standalone terminal environments where error output should be separated from standard data output streams without incurring framework bootstrapping costs.
- Existing validation routines rely on direct runtime console error and warning calls rather than introducing external logging client dependencies or centralized telemetry pipelines.

## Problem Statement

Repository operational and verification scripts lack a standardized architecture for reporting runtime errors and operational diagnostics, leading to ad-hoc invocations of runtime console methods without structured log levels, consistent payload formatting, or decoupled output destinations.

## Decision

1. MUST: Engineers introducing or updating script dependencies MUST inspect the project lock artifact to verify the exact resolved version against the dependency manifest before using dependency APIs.

## Policy Block

- MUST Engineers introducing or updating script dependencies MUST inspect the project lock artifact to verify the exact resolved version against the dependency manifest before using dependency APIs.

In scope:
- Operational, verification, and repository maintenance scripts executing in standalone execution contexts.
- Diagnostic, warning, and failure reporting within automated validation routines.

Out of scope:
- Published library source modules intended for external consumption.
- Long-running daemon services requiring structured distributed tracing or aggregated telemetry sinks.

Exceptions:
- EXC-001: A script requires structured machine-readable log ingestion into an external operational collector.

## Rationale

- Direct runtime console error and warning output avoids adding runtime dependencies to standalone maintenance scripts, keeping script execution lightweight and decoupled.
- Directing failure diagnostics to the standard error stream preserves Unix stream separation, allowing calling environments to distinguish script error output from data pipeline streams.
- Standardizing on native runtime console facilities aligns with the observed pattern across existing repository verification scripts.

## Consequences

Positive:
- Zero external dependency footprint and zero initialization overhead for standalone repository scripts.
- Consistent separation between operational standard output and diagnostic standard error streams.
- Immediate visibility of failure contexts and remediation instructions in terminal environments.

Negative:
- Absence of structured machine-parsable log records for automated log aggregation systems.
- No configurable log level thresholds or global filtering mechanisms without custom environment evaluation logic.
- Limited ability to redirect log streams to remote observability backends without shell-level stream redirection.

## Alternatives

- Adopt an external structured logging library across all repository scripts (rejected)
  Rejected because: Introducing an external logging package adds dependency maintenance overhead and initialization complexity without providing proportionate value for standalone verification checks.
  When valid: When scripts become persistent background services requiring structured telemetry aggregation and remote transport pipelines.
- Route all messages through standard output using basic printing functions (rejected)
  Rejected because: Emitting errors to standard output prevents downstream automated pipelines from distinguishing normal execution payloads from failure diagnostics.
  When valid: When execution output is strictly intended for unstructured human reading without pipeline orchestration.

## Risks

- Inconsistent diagnostic formatting across different scripts could make automated failure parsing difficult.
  Mitigation: Establish standard message structures with explicit prefix indicators for errors and warnings in script templates.
  Owner: engineering team
- Scripts may leak sensitive environment details or credentials when dumping diagnostic objects to standard error.
  Mitigation: Sanitize all dynamic values and environment variables before interpolating them into console diagnostic messages.
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
- Construct error diagnostic strings with explicit failure summaries followed by actionable remediation steps.
- Ensure script processes return non-zero exit codes whenever terminal failure messages are emitted to the error stream.

## Continuation Context


Verify commands:
- Discover the repository project manifest, identify configured script verification tasks, and execute the verification suite to ensure all script checks pass.
- Inspect the script runner configuration and execute the static code analysis suite to verify error stream logging compliance.

Accept when:
- All repository verification and maintenance scripts execute without throwing unhandled exceptions.
- Script failures and rule violations emit formatted diagnostics exclusively to the standard error stream.
- Process exit status accurately reflects the execution outcome indicated by the emitted console stream.

## Enforcement

- Verified by: Automated continuous integration pipeline executing repository verification and static check scripts.
- Verified by: Peer code review for all new and modified repository scripts.
- Violation handling: Continuous integration checks fail when verification scripts encounter unhandled error conditions.
- Violation handling: Pull requests introducing external logging dependencies or routing script errors to standard output are blocked.
- Exception process: Submit an architectural review request detailing why native runtime console error streams cannot satisfy operational telemetry requirements.