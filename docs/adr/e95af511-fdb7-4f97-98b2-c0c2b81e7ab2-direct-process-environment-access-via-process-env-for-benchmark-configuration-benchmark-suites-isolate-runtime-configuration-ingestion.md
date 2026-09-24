# Direct Process Environment Access via process.env for Benchmark Configuration: Benchmark Suites Isolate Runtime Configuration Ingestion

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Performance benchmarking scripts require configuration toggles to selectively filter, parameterize, or trigger specific benchmark executions at runtime.
- The benchmarking harness directly reads runtime environment variables through the global process.env structure without intermediary schema validation or centralized secrets management facilities.
- Static inspection identified ambient environment property evaluation within benchmarking execution workflows, raising potential governance concerns regarding configuration and credential boundary management.

## Problem Statement

Direct, unvalidated access to ambient runtime environment variables creates untracked configuration dependencies and risks accidental exposure of sensitive environment variables when benchmark outputs or execution traces are logged.

## Decision

1. MUST: Benchmark suites MUST isolate runtime configuration ingestion by defining explicit, typed configuration schemas rather than reading unvalidated global process.env properties directly across benchmark execution files.

## Policy Block

- MUST Benchmark suites MUST isolate runtime configuration ingestion by defining explicit, typed configuration schemas rather than reading unvalidated global process.env properties directly across benchmark execution files.

In scope:
- Performance benchmarking harnesses and test suites requiring runtime execution toggles or filter configurations.

Out of scope:
- Core production application runtime services and shared infrastructure libraries that utilize dedicated secret management stores.

## Rationale

- Direct reads of ambient environment variables in localized benchmarking scripts bypass centralized configuration boundaries and risk leaking sensitive environment variables into printed benchmark tables.
- Explicitly defining expected configuration parameters prevents unexpected benchmark behaviors caused by undefined or malformed ambient environment values.
- The current evidence represents an isolated, single-file access pattern in a benchmark harness, requiring minimal formal boundary constraints without imposing heavyweight enterprise secrets infrastructure on standalone performance tests.

## Consequences

Positive:
- Prevents accidental leakage of ambient environment variables and credentials during benchmark table printing and console reporting.
- Establishes predictable and validated parameter inputs for benchmarking runs.
- Decouples benchmark execution logic from specific ambient runtime environment keys.

Negative:
- Requires boilerplate schema definition or configuration wrapping for simple benchmark execution toggles.
- Increases initial setup effort when creating temporary ad-hoc benchmark harnesses.

## Alternatives

- Adopting a dedicated external secrets manager for benchmark parameterization (rejected)
  Rejected because: External secrets managers introduce unnecessary network latency, credentials bootstrap requirements, and operational overhead for ephemeral, non-sensitive benchmark flags.
  When valid: When benchmarks interact with authenticated external production-like test services requiring real service credentials.
- Permitting unconstrained global process.env access across all benchmark scripts (rejected)
  Rejected because: Unchecked ambient environment access leads to fragmented configuration sources and increases the risk of leaking sensitive tokens in test output tables.
  When valid: During initial prototyping before code is committed to shared repository repositories.

## Risks

- Developers may unintentionally log ambient environment values when printing benchmark performance summary tables.
  Mitigation: Enforce strict schema validation and automated linting that prevents printing ambient runtime environment variables.
  Owner: engineering team
- Over-constraining test configurations could increase friction for running quick local benchmark experiments.
  Mitigation: Provide permissive defaults with clear fallbacks in the benchmark configuration schema.
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
- Encapsulate benchmark configuration parsing in a dedicated setup module that sanitizes input parameters before instantiating benchmark suites.
- Verify that benchmark reporting formatters only include benchmark timing statistics and exclude raw runtime configuration objects from final tabular outputs.

## Continuation Context


Verify commands:
- Discover the repository static analysis and security scanning script from the root manifest and run it to verify no sensitive credentials or direct ambient environment variables are leaked in benchmark reporting.
- Locate the benchmark test execution script defined in the project manifest and execute the test runner to validate configuration schema handling.

Accept when:
- Static analysis checks pass without flagging unauthorized ambient environment variable reads or unredacted credential exposures.
- Benchmark execution completes successfully using defined configuration defaults when ambient environment variables are unset.

## Enforcement

- Verified by: Automated static analysis checks in the continuous integration pipeline scanning for raw process.env access.
- Verified by: Peer code review during merge request evaluation.
- Violation handling: Continuous integration builds fail upon detection of raw ambient environment reads outside sanctioned configuration boundary modules.
- Violation handling: Pull requests containing unvalidated environment variable access must be revised to use the central configuration module.
- Exception process: Temporary exceptions for local exploratory benchmarking require written justification and sign-off from the security and architecture teams.