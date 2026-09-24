# metabench Internal Module Adoption: Benchmark Test Suites Standardize Internal Metabench

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Performance evaluation across data validation and transformation modules requires repeatable measurement harnesses with consistent timing characteristics.
- Benchmark suites across the codebase require a unified execution harness rather than fragmented third-party test runners to ensure comparable performance metrics.
- Internal modules within the repository provide shared benchmark lifecycle orchestration and execution telemetry across performance evaluation suites.

## Problem Statement

Benchmarking data validation operations across diverse workloads requires consistent timing measurement, lifecycle management, and warm-up cycles. Disparate benchmark configurations introduce measurement divergence and runner overhead, making performance regressions difficult to detect and isolate without a standardized internal harness.

## Decision

1. MUST: Benchmark test suites MUST standardize on the internal metabench module as the shared harness for orchestrating benchmark execution cycles and collecting performance telemetry.

## Policy Block

- MUST Benchmark test suites MUST standardize on the internal metabench module as the shared harness for orchestrating benchmark execution cycles and collecting performance telemetry.

In scope:
- Performance evaluation test suites and benchmark suites within the repository.
- Benchmark modules measuring data validation, transformation, and parse operations.

Out of scope:
- Standard unit and integration test suites that verify functional behavior rather than execution throughput.
- Production application runtime modules.

Exceptions:
- EXC-20-001: A benchmark suite requires low-level kernel profiling or external instrumentation not supported by the harness interface.

## Rationale

- Adopting the internal metabench module guarantees consistent execution cycles, statistical sampling, and measurement baselines across all benchmark suites.
- Centralizing benchmark orchestration eliminates duplicated timing and reporting logic across performance evaluation suites.
- Internal harness ownership allows performance measurement contracts to evolve in lockstep with the core codebase requirements.

## Consequences

Positive:
- Unified benchmark telemetry and comparable throughput metrics across all evaluated workloads.
- Reduced boilerplate and eliminated redundant timing code across performance measurement suites.
- Direct control over benchmark warm-up cycles, statistical sampling, and environment normalization.

Negative:
- Ongoing maintenance overhead required to maintain and evolve an internal benchmarking harness module.
- Tighter architectural coupling between benchmark definition suites and the custom harness interface.

## Alternatives

- Adopt an external microbenchmarking library from public package registries. (rejected)
  Rejected because: External libraries introduce external dependency churn, mismatched reporting conventions, and less flexibility for custom suite configurations.
  When valid: When standard external reporting formats are mandatory across external organizational boundaries or when internal harness maintenance is unviable.
- Implement ad-hoc execution loops and timers within each individual benchmark suite. (rejected)
  Rejected because: Ad-hoc loops cause inconsistent warm-up handling, irregular iteration counts, and incomparable performance metrics across suites.
  When valid: When performing one-off exploratory profiling during local investigation.

## Risks

- Divergence between the internal harness execution model and emerging runtime profiling primitives.
  Mitigation: Review harness timing mechanics periodically against runtime platform updates and benchmark measurement standards.
  Owner: Engineering team
- Benchmark suites bypassing harness abstractions to access internal execution internals.
  Mitigation: Enforce strict module boundary checks and code reviews on benchmark suite imports.
  Owner: Engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Benchmark suites should import the internal harness module directly and pass benchmark task definitions into the runner registration interface.
- Companion benchmark utilities should be utilized for input generation and fixture preparation prior to entering timed execution blocks.

## Continuation Context


Verify commands:
- Discover the project benchmark script defined in the dependency manifest and execute it to run all performance suites.
- Inspect the build and lint scripts in the repository configuration to verify static module boundary compliance across benchmark suites.

Accept when:
- All benchmark suites execute successfully through the standardized harness runner without unhandled lifecycle rejections.
- Static boundary checks confirm benchmark suites rely solely on authorized internal harness and utility modules.

## Enforcement

- Verified by: Automated continuous integration benchmark execution pipelines.
- Verified by: Peer code review for all modifications or additions to benchmark suites.
- Violation handling: Automated pull request checks fail if unapproved benchmarking harnesses or ad-hoc timing routines are introduced.
- Violation handling: Reviewers require refactoring of ad-hoc benchmark scripts to utilize the standard harness module.
- Exception process: Submit an architectural review request outlining the specialized profiling requirement that cannot be accommodated by the standard harness.
- Exception process: Obtain sign-off from the technical lead prior to merging custom profiling hooks.