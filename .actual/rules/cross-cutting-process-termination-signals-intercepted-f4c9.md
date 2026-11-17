---
version: 2
name: cross-cutting-process-termination-signals-intercepted-f4c9
description: "Benchmark Suite Event-Driven Lifecycle Integration: Process Termination Signals Intercepted Dedicated Signal"
metadata:
  actual:
    adr_id: f4c9a667-de94-41f5-ac5a-01c16ee8f8d1
    status: accepted
    candidate_group_id: 58e9da9d-b094-48a3-acf6-7db168163a94
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Suite Event-Driven Lifecycle Integration: Process Termination Signals Intercepted Dedicated Signal

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for benchmark test suites and performance measurement modules utilizing the benchmark library.

### Rules

- **R-BE-001** MAY: Process termination signals MAY be intercepted with dedicated process signal event listeners to ensure graceful exit during active benchmark iterations.

### Verify

```bash
# Discover the repository benchmark script defined in the dependency manifest and execute it to verify suite cycle output.
# Inspect benchmark suite definitions to ensure test lambdas do not contain standard input and output or logging statements.
```

**Accept when:**
- Benchmark suites execute and emit cycle events reporting target completion without throwing unhandled exceptions.
- All benchmark suites register cycle event listeners via the on method and exclude logging logic from add test lambdas.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis and code review checks verifying that benchmark suites use suite cycle event listeners and continuous integration test runs ensuring all benchmark suites run to completion without unhandled callback errors.
</enforcement>