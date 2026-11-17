---
version: 2
name: eb41e130-efb4-4e71-a52f-0b804f9b42f7-adoption-of-execa-for-subprocess-execution-in-benchmark-suites-before-implementing-updating-process-execution-logic
description: "Adoption of execa for Subprocess Execution in Benchmark Suites: Before Implementing Updating Process Execution Logic"
metadata:
  actual:
    adr_id: eb41e130-efb4-4e71-a52f-0b804f9b42f7
    status: accepted
    candidate_group_id: 732ee91a-e074-4c4e-bb43-f12941fb2992
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Adoption of execa for Subprocess Execution in Benchmark Suites: Before Implementing Updating Process Execution Logic

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/tsc`

Applies to:
- `bench/**`

## Context

- Performance benchmarking suites require programmatic execution of compiler processes across diverse test workloads.
- Direct invocation of standard runtime process spawning primitives across disparate benchmark suites introduces inconsistent stream handling, error propagation, and termination semantics.
- The codebase demonstrates repeated adoption of execa within benchmark harnesses to coordinate process execution uniformly.

## Problem Statement

Benchmark suites that execute child processes without a consistent process management library risk divergent process lifecycle management, unhandled stream buffers, and platform-specific execution failures across benchmark runs.

## Decision

1. MUST: Before implementing or updating process execution logic with execa, consumers MUST inspect the repository lock artifact to identify the exact resolved version and adhere to its published API contracts.

## Policy Block

- MUST Before implementing or updating process execution logic with execa, consumers MUST inspect the repository lock artifact to identify the exact resolved version and adhere to its published API contracts.

In scope:
- Benchmark harness suites and performance measurement suites executing external processes
- Integration benchmarks requiring programmatic compiler process invocation

Out of scope:
- In-memory unit tests and pure function test suites
- Core runtime library exports distributed to external consumers

## Rationale

- Adopting execa across benchmark modules unifies process creation, stream management, and error handling into a single standardized interface.
- Observed pattern consistency across benchmark files verifies that centralizing child process mechanics reduces duplicated process harness logic.
- Promise-oriented process execution improves synchronization and deterministic measurement of compiler workloads across different benchmarking scenarios.

## Consequences

Positive:
- Standardizes process stream management and exit code handling across all performance benchmark suites.
- Reduces boilerplate code required to launch, monitor, and clean up external compiler benchmark executions.
- Provides consistent promise-based process invocation that simplifies asynchronous benchmark orchestration.

Negative:
- Introduces an external dependency that must be maintained and tracked in the repository dependency resolution manifest.
- Benchmark authors must adhere to library-specific execution semantics and configuration options rather than runtime defaults.

## Alternatives

- Standard runtime child process execution modules (rejected)
  Rejected because: Standard runtime process modules require manual promise wrapping, custom stream buffering, and verbose lifecycle error handling across every benchmark suite.
  When valid: Valid when eliminating all third-party module dependencies is an overriding project constraint.
- Custom internal process management wrapper around runtime primitives (rejected)
  Rejected because: Maintaining an internal process execution wrapper introduces additional engineering overhead when established libraries already solve cross-platform process isolation.
  When valid: Valid when proprietary platform-specific process sandboxing features are required.

## Risks

- Breaking API changes across major version updates of the external process execution library.
  Mitigation: Adhere to the discovery policy by grounding usage against the exact resolved version recorded in the repository lock artifact and validating benchmark execution before dependency upgrades.
  Owner: engineering team
- Child process zombie leaks or hung executions stalling automated continuous benchmark runners.
  Mitigation: Enforce explicit process timeout configurations and graceful signal termination on all execa invocations.
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
- Benchmark suites should encapsulate shared fixture generation and parameter setup in reusable helper modules before invoking execa for compiler execution.
- Process outputs should be inspected for error exit codes and process signal terminations to ensure benchmark metrics only record successful executions.

## Continuation Context


Verify commands:
- Discover the benchmark execution task in the project task configuration and run the benchmark suite to verify child process execution.
- Inspect repository dependency declarations to confirm execa is declared within the appropriate workspace dependency scope.

Accept when:
- All benchmark execution suites spawn external processes through execa without runtime failures.
- Automated benchmark runs complete with deterministic exit codes and clean child process termination.

## Enforcement

- Verified by: Automated continuous integration pipeline execution of benchmark suites
- Verified by: Static code review verifying process invocation compliance across benchmark modules
- Violation handling: Direct calls to unapproved process execution primitives block code review approval
- Violation handling: Unmanaged process spawning identified during review must be refactored to use execa
- Exception process: Exceptions require approval from benchmark harness maintainers with documented technical justification.