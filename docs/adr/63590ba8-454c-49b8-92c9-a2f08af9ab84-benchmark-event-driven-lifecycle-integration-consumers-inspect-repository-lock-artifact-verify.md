# benchmark Event-Driven Lifecycle Integration: Consumers Inspect Repository Lock Artifact Verify

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Performance benchmarking requires predictable lifecycle observability to monitor iterative progress across individual test iterations.
- Standardized event handlers enable comparative analysis across distinct execution strategies by capturing throughput and variance metrics.
- Aggregating individual run statistics at the completion boundary provides relative performance baselines without altering benchmark execution logic.

## Problem Statement

Performance suites require decoupled mechanisms to monitor test iterations in real time and compile comparative execution statistics upon completion without polluting benchmarking loops.

## Decision

1. MUST: Consumers MUST inspect the repository lock artifact to verify the exact resolved version of the benchmark library prior to implementing or modifying benchmark suites.

## Policy Block

- MUST Consumers MUST inspect the repository lock artifact to verify the exact resolved version of the benchmark library prior to implementing or modifying benchmark suites.

In scope:
- Performance benchmarking suites and execution harnesses within the project.

Out of scope:
- Functional unit tests, integration tests, and production runtime code paths.

## Rationale

- Subscribing to cycle and complete events decouples benchmark measurement loops from reporting and presentation logic.
- Structured event aggregation allows computing relative throughput ratios and statistical variance across all executed variants in a single pass.
- Centralizing metrics formatting at the suite completion boundary prevents measurement skew during active iteration phases.

## Consequences

Positive:
- Clear separation between performance execution logic and result formatting.
- Consistent reporting of throughput, mean duration, and margin of error across suites.
- Real-time visibility into individual benchmark iterations as they finish.

Negative:
- Coupling to the specific event lifecycle and suite API exposed by the benchmarking library.
- Overhead of maintaining custom result aggregation and tabular formatting code within benchmark harnesses.

## Alternatives

- Ad-hoc manual console logging within individual benchmark iteration loops (rejected)
  Rejected because: Introduces significant measurement skew and fails to aggregate comparative summary metrics across iterations
  When valid: Exploratory single-run script debugging where statistical accuracy is not required
- Relying strictly on default unformatted runner text output (rejected)
  Rejected because: Lacks custom tabular comparative calculations such as relative speed multipliers against the slowest variant
  When valid: Environments where terminal formatting libraries cannot be resolved

## Risks

- Event handler execution overhead could perturb statistical accuracy if handlers run synchronously within measurement cycles
  Mitigation: Ensure heavy calculation and table formatting occur exclusively within the complete event rather than per-iteration cycle callbacks
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
- Attach cycle listeners solely for minimal progress logging, deferring summary transformations until the complete event fires.
- Extract throughput, mean execution time, relative margin of error, and sample count directly from benchmark suite event targets.

## Continuation Context


Verify commands:
- Discover and run the project benchmark suite script defined in the repository configuration.
- Inspect benchmark execution output to confirm cycle progress and completion tables render without errors.

Accept when:
- Benchmark suite runs to completion and emits cycle notifications followed by a tabular summary.
- Reported metrics contain throughput, mean duration, and error margin calculations.

## Enforcement

- Verified by: Automated continuous integration runs executing project benchmark validation tasks.
- Verified by: Peer code review of benchmark harness additions and event subscriptions.
- Violation handling: Rejection of pull requests introducing unmanaged benchmarking loops without lifecycle event handling.
- Exception process: Submit an architectural review request documenting why alternative benchmark runners or headless metric exporters are required.