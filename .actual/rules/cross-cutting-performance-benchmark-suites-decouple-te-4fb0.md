---
version: 2
name: cross-cutting-performance-benchmark-suites-decouple-te-4fb0
description: "Benchmark Suite Event-Driven Lifecycle Integration: Performance Benchmark Suites Decouple Test Execution"
metadata:
  actual:
    adr_id: 4fb0931d-0bc6-49d5-b26c-92bd4c548a5f
    status: accepted
    candidate_group_id: 58e9da9d-b094-48a3-acf6-7db168163a94
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Suite Event-Driven Lifecycle Integration: Performance Benchmark Suites Decouple Test Execution

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for:
- Benchmark test suites and performance measurement modules utilizing the benchmark library.

### Rules

- **R-IP-001** MUST: Performance benchmark suites MUST decouple test execution loops from cycle telemetry by subscribing to the benchmark suite cycle event using the on method rather than embedding reporting logic inside benchmark test functions.

### Verify

- Discover the repository benchmark script defined in the dependency manifest and execute it to verify suite cycle output.
- Inspect benchmark suite definitions to ensure test lambdas do not contain standard input and output or logging statements.

**Accept when:**

- Benchmark suites execute and emit cycle events reporting target completion without throwing unhandled exceptions.
- All benchmark suites register cycle event listeners via the on method and exclude logging logic from add test lambdas.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis and code review checks verifying that benchmark suites use suite cycle event listeners.
- Verified by: Continuous integration test runs ensuring all benchmark suites run to completion without unhandled callback errors.
- Violation handling: Pull requests containing inline logging inside benchmark case definitions or missing cycle event listeners must be revised before merge.
- Exception process: Exceptions require documented architectural justification and sign-off from the performance engineering team.
</enforcement>
