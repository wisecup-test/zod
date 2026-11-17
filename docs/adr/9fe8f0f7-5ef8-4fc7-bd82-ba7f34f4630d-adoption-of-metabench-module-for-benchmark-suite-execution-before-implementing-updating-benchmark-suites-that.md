---
version: 2
name: 9fe8f0f7-5ef8-4fc7-bd82-ba7f34f4630d-adoption-of-metabench-module-for-benchmark-suite-execution-before-implementing-updating-benchmark-suites-that
description: "Adoption of metabench Module for Benchmark Suite Execution: Before Implementing Updating Benchmark Suites That"
metadata:
  actual:
    adr_id: 9fe8f0f7-5ef8-4fc7-bd82-ba7f34f4630d
    status: accepted
    candidate_group_id: b9904703-b2ce-4b3d-91ac-98c45f380b73
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
---

# Adoption of metabench Module for Benchmark Suite Execution: Before Implementing Updating Benchmark Suites That

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `packages/bench/**`

## Context

- The repository maintains performance benchmarking suites requiring consistent harness execution and reproducible timing measurement across numerous test cases.
- Standardizing benchmark execution through the shared metabench module ensures uniform micro-benchmark lifecycle management and isolated measurement execution.
- Benchmark suites benefit from unified measurement methodology rather than fragmented benchmarking execution patterns across different suites.

## Problem Statement

Performance benchmarking suites across the repository require a single, consistent execution harness to ensure measurements remain comparable, reproducible, and decoupled from divergent runner implementations.

## Decision

1. MUST: Before implementing or updating benchmark suites that rely on dependencies, consumers MUST discover the repository dependency manifest and inspect the authoritative lock artifact to verify resolved dependency versions against official documentation.

## Policy Block

- MUST Before implementing or updating benchmark suites that rely on dependencies, consumers MUST discover the repository dependency manifest and inspect the authoritative lock artifact to verify resolved dependency versions against official documentation.

In scope:
- Performance benchmarking suites and micro-benchmark test cases within the repository.
- Execution harness orchestration and performance measurement cycles.

Out of scope:
- Unit test suites and functional integration test suites.
- Production runtime application code and non-benchmarking modules.

## Rationale

- Evidence from seventeen benchmark files demonstrates recurring adoption of the internal metabench module for coordinating benchmark suite execution.
- Centralizing benchmark harness execution eliminates fragmented benchmarking logic and ensures uniform execution semantics across performance suites.
- Standardized harness boundaries allow the engineering team to optimize benchmark execution overhead without refactoring individual benchmark cases.

## Consequences

Positive:
- Provides uniform measurement semantics and comparable performance data across all repository benchmark suites.
- Reduces boilerplate configuration by centralizing benchmark harness lifecycle management in a shared module.
- Simplifies benchmark authoring by providing consistent harness interfaces across different benchmark cases.

Negative:
- Creates a dependency on internal module maintenance for all benchmarking execution requirements.
- Requires benchmark authors to adhere strictly to harness execution conventions rather than using arbitrary measurement loops.

## Alternatives

- Independent custom timing loops implemented per benchmark suite (rejected)
  Rejected because: Leads to inconsistent timing methodologies, redundant harness code, and incomparable metrics across suites.
  When valid: Valid only in standalone single-file scratchpads that are not part of the integrated repository benchmark suite.
- Adopting third-party benchmarking runner frameworks (rejected)
  Rejected because: Introduces external runtime dependencies and differing harness requirements that diverge from the repository internal benchmarking architecture.
  When valid: Valid if the project establishes an ecosystem-wide mandate for an external benchmarking runner across all packages.

## Risks

- Changes to the internal metabench harness interface could break existing benchmark suites across the repository.
  Mitigation: Treat the internal metabench interface as a stable contract and validate all benchmark suites against interface changes during verification cycles.
  Owner: Engineering Team
- Harness execution overhead could skew micro-benchmark measurements if not calibrated correctly.
  Mitigation: Isolate harness lifecycle timing from benchmark workload execution and benchmark the harness itself periodically.
  Owner: Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Import the internal metabench module to structure benchmark cases, separating benchmark setup logic from timed iteration blocks.
- Maintain auxiliary utility functions in dedicated utility modules while delegating all measurement harness coordination exclusively to the metabench module.

## Continuation Context


Verify commands:
- Discover the repository configuration and execute the designated benchmark verification script to validate benchmark suite execution.
- Discover and run the project static type-checking and linting scripts to verify compliance with internal module import conventions.

Accept when:
- All benchmark suites execute successfully through the metabench harness without execution errors.
- Benchmark suite definitions adhere to module import constraints and static type validation passes across all benchmark modules.

## Enforcement

- Verified by: Automated continuous integration pipeline running repository benchmark validation scripts.
- Verified by: Code review inspection of benchmark suites to ensure exclusive use of the metabench harness.
- Violation handling: Pull requests introducing ad-hoc benchmark runners or bypassing the metabench harness will fail code review and automated checks.
- Exception process: Exceptions must be requested through an architecture review proposal detailing why the metabench module cannot support the specific benchmark requirement.