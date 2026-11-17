---
version: 2
name: a110d8e6-6c89-42d7-86eb-fe5c5fb350b8-adoption-of-benchmark-library-for-performance-measurement-suites-benchmark-suites-attach-cycle-listeners-via
description: "Adoption of benchmark Library for Performance Measurement Suites: Benchmark Suites Attach Cycle Listeners Via"
metadata:
  actual:
    adr_id: a110d8e6-6c89-42d7-86eb-fe5c5fb350b8
    status: accepted
    candidate_group_id: a40953fe-dded-4098-9e8e-51ebfac73e1a
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Adoption of benchmark Library for Performance Measurement Suites: Benchmark Suites Attach Cycle Listeners Via

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v3/benchmarks/**`

## Context

- Microbenchmarking of parsing and validation throughput requires isolated, statistically stable execution environments across varied input shapes.
- Core validation primitives, object parsing schemas, union discriminators, and string operations exhibit distinct performance profiles requiring continuous regression tracking.
- The codebase establishes dedicated benchmark suites configured with standardized cycle event monitoring and error handling for invalid input iterations.

## Problem Statement

Manual execution timing produces variable results that fail to isolate parser overhead and algorithmic regressions across valid, invalid, and edge-case validation payloads.

## Decision

1. SHOULD: Benchmark suites SHOULD attach cycle listeners via the `on` method with the cycle event parameter to record standardized per-scenario throughput diagnostics.

## Policy Block

- SHOULD Benchmark suites SHOULD attach cycle listeners via the `on` method with the cycle event parameter to record standardized per-scenario throughput diagnostics.

In scope:
- Validation routines, schema parsing modules, and primitive evaluation routines undergoing performance evaluation
- Automated benchmark execution harnesses and regression measurement suites

Out of scope:
- Functional and unit testing suites verifying validation correctness
- Production runtime schema compilation and execution logic

## Rationale

- Adopting a dedicated benchmarking library provides statistically controlled sampling, warmup cycles, and variance reduction across execution runs.
- Consistent suite patterns using chained registration and cycle event hooks establish unified diagnostic output across all data type validation tests.
- Encapsulating negative schema execution in localized error handlers ensures benchmark completion while capturing invalid input parsing overhead.

## Consequences

Positive:
- Provides repeatable, high-precision measurement of schema parsing throughput and execution overhead.
- Standardizes cycle event diagnostics facilitating automated performance regression tracking across revisions.
- Isolates computational bottlenecks in primitive validation, object parsing, and union resolution early in the development lifecycle.

Negative:
- Incurs ongoing maintenance overhead for dedicated benchmark harnesses alongside regular test suites.
- Poses risk of synthetic microbenchmarks optimizing for artificial hot paths that diverge from realistic production payload distributions.

## Alternatives

- Ad-hoc execution timing using runtime monotonic clock timestamps (rejected)
  Rejected because: Lacks automated statistical warmups, iteration scaling, and variance mitigation, resulting in high measurement jitter.
  When valid: Valid only for rough preliminary timing checks during exploratory development spikes.
- Standard unit test framework execution timing (rejected)
  Rejected because: Unit test runners prioritize assertion correctness over statistical sampling loops and cycle throughput normalization.
  When valid: Valid when testing for binary execution time limits rather than micro-operations per second.

## Risks

- Synthetic benchmark scenarios diverge from real-world schema payloads, yielding deceptive performance metrics.
  Mitigation: Incorporate realistic multi-field payload fixtures alongside isolated primitive microbenchmarks.
  Owner: engineering team
- Uncaught exceptions during negative benchmark scenarios terminate the entire suite process prematurely.
  Mitigation: Enforce defensive error containment within all benchmark iteration callbacks targeting invalid input paths.
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
- Discover the benchmarking layout within the workspace and register new validation scenarios by extending existing suite declarations.
- Ensure error containment structures around negative validation benchmarks mirror schema exception types without swallowing fatal runtime signals.

## Continuation Context


Verify commands:
- echo "Discover and execute project benchmark verification scripts from configuration artifacts"

Accept when:
- All benchmark suites complete execution cycles without unhandled exceptions.
- Cycle event listeners log target operations per second for all registered validation scenarios.

## Enforcement

- Verified by: Automated continuous integration pipeline execution of benchmark verification targets.
- Verified by: Peer code review for all new schema primitives and parsing performance test cases.
- Violation handling: Pull requests introducing validation primitives without corresponding benchmark coverage are blocked from merging.
- Violation handling: Benchmark execution failures or unhandled cycle errors fail the continuous integration build.
- Exception process: Exceptions require documented architectural justification and explicit sign-off from the technical lead.