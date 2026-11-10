---
version: 2
name: ee7b2879-0b5a-4553-85b3-bebdb81b8bc0-benchmark-library-adoption-for-schema-performance-evaluation-before-implementing-modifying-benchmark-suites-engineers
description: "Benchmark Library Adoption for Schema Performance Evaluation: Before Implementing Modifying Benchmark Suites Engineers"
metadata:
  actual:
    adr_id: ee7b2879-0b5a-4553-85b3-bebdb81b8bc0
    status: accepted
    candidate_group_id: f25aea77-f01a-48e5-8bc3-2e219c7a9c40
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Library Adoption for Schema Performance Evaluation: Before Implementing Modifying Benchmark Suites Engineers

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v3/benchmarks/**`

## Context

- High-throughput data parsing and schema validation require low-overhead execution to prevent latency bottlenecks in runtime applications.
- Validation performance varies significantly across primitive types, composite objects, unions, and error-handling paths.
- Manual timestamp profiling yields noisy, non-reproducible measurements due to runtime optimization cycles and evaluation artifacts.

## Problem Statement

Measuring parser throughput and execution overhead across primitive and composite schemas requires a standardized benchmarking harness that isolates valid parsing from exception handling while providing statistically robust iteration timing.

## Decision

1. MUST: Before implementing or modifying benchmark suites, engineers MUST inspect the repository lock artifact to determine the exact resolved version of the benchmark library and verify API compatibility against authoritative documentation.

## Policy Block

- MUST Before implementing or modifying benchmark suites, engineers MUST inspect the repository lock artifact to determine the exact resolved version of the benchmark library and verify API compatibility against authoritative documentation.

In scope:
- Performance evaluation and throughput profiling of schema parsing and validation functions.
- Regression analysis of core primitive and composite data structure parsers.

Out of scope:
- Functional correctness assertions and end-to-end integration tests.
- Non-performance-critical utility routines.

## Rationale

- Statistically rigorous benchmarking requires controlled execution cycles and iteration warming that standard ad-hoc timers cannot provide.
- Standardizing on benchmark suite methods provides a consistent interface for registering valid parsing paths and expected failure branches.
- Capturing cycle events enables centralized emission of operations-per-second metrics across diverse schema configurations.

## Consequences

Positive:
- Provides reproducible, statistically sound throughput metrics for schema parsing across diverse payload shapes.
- Enables precise detection of parsing latency regressions across primitive and complex composite schemas.
- Separates performance benchmarking harnesses from functional test assertions.

Negative:
- Dedicated benchmark suites require ongoing synchronization as schema validation interfaces and parsing semantics evolve.
- Comprehensive benchmark test runs introduce additional compute duration into performance validation workflows.

## Alternatives

- Ad-hoc execution timing using standard runtime timestamp deltas (rejected)
  Rejected because: Fails to account for statistical variance, engine warm-up cycles, garbage collection pauses, and execution iteration scale.
  When valid: Acceptable only for informal one-off local script diagnostics where statistical rigor is unnecessary.
- Generic unit test assertions with coarse timing boundaries (rejected)
  Rejected because: Couples assertion testing with performance measurement and introduces assertion evaluation overhead into performance numbers.
  When valid: Acceptable for regression thresholds where binary pass-fail execution latency suffices without granular throughput analysis.

## Risks

- Benchmark suites may measure harness overhead rather than parser execution time if test closures contain extraneous logic.
  Mitigation: Isolate parse execution targets inside tightly scoped closures and separate successful parses from error-catching branches.
  Owner: engineering team
- Fluctuations in host hardware environments can introduce variance into benchmark comparisons across runs.
  Mitigation: Execute performance benchmarks in standardized environments with fixed resource limits.
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
- Ensure test payloads represent both minimal and fully populated data structures to measure parsing boundaries accurately.
- Keep benchmark scenario definitions isolated to avoid cross-suite state contamination during cycle execution.

## Continuation Context


Verify commands:
- Discover the performance test script declared in the repository dependency manifest and execute it using the project-designated task runner.
- Inspect the repository task configuration to locate and trigger the benchmark suite execution workflow.

Accept when:
- All benchmark test suites execute to completion through their registered cycle event handlers without uncaught exceptions.
- Validation parse operations within benchmark cases accurately reflect real-world payload shapes and error conditions.

## Enforcement

- Verified by: Automated performance validation workflows triggered during release verification phases.
- Verified by: Peer code review verifying that schema additions include corresponding benchmark coverage.
- Violation handling: Pull requests introducing unbenchmarked core parsing alterations or ad-hoc timing loops are blocked during review.
- Violation handling: Benchmark suites failing cycle execution or throwing unhandled errors require immediate remediation prior to merge.
- Exception process: Submit an architectural exception request detailing why standardized benchmarking cannot be applied to the specific schema validation path.
- Exception process: Secure approval from the performance engineering group and document the alternative evaluation methodology in repository documentation.