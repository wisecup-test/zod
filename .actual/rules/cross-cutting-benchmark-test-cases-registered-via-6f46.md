---
version: 2
name: cross-cutting-benchmark-test-cases-registered-via-6f46
description: "Benchmark Suite Event-Driven Lifecycle Integration: Benchmark Test Cases Registered Via Add"
metadata:
  actual:
    adr_id: 6f4629d5-fada-455d-9892-96adf197b35e
    status: accepted
    candidate_group_id: 58e9da9d-b094-48a3-acf6-7db168163a94
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Suite Event-Driven Lifecycle Integration: Benchmark Test Cases Registered Via Add

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for benchmark test suites and performance measurement modules utilizing the benchmark library.

### Rules

- **R-BENCH-001** MUST_NOT: Benchmark test cases registered via the add method MUST NOT perform console logging or telemetry aggregation inside the measured execution lambda.

### Verify

```bash
# Discover the repository benchmark script defined in the dependency manifest and execute it to verify suite cycle output.
# Inspect benchmark suite definitions to ensure test lambdas do not contain standard input and output or logging statements.
```

**Accept when:**
- Benchmark suites execute and emit cycle events reporting target completion without throwing unhandled exceptions.
- All benchmark suites register cycle event listeners via the on method and exclude logging logic from add test lambdas.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis, code review checks, and continuous integration test runs ensuring all benchmark suites run to completion without unhandled callback errors.
</enforcement>