---
version: 2
name: cross-cutting-before-utilizing-benchmark-library-modif-c1a5
description: "Benchmark Suite Event-Driven Lifecycle Integration: Before Utilizing Benchmark Library Modifying Suite"
metadata:
  actual:
    adr_id: c1a59675-30b3-461c-92eb-6f71a3e4e437
    status: accepted
    candidate_group_id: 58e9da9d-b094-48a3-acf6-7db168163a94
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Suite Event-Driven Lifecycle Integration: Before Utilizing Benchmark Library Modifying Suite

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for all benchmark test suites and performance measurement modules utilizing the benchmark library.

### Rules

- **R-BMK-001** MUST: Before utilizing the benchmark library or modifying suite execution logic, engineers MUST inspect the repository dependency manifest and lock artifact to resolve the exact locked version of the benchmark library.
- **R-BMK-002** MUST: Register cycle event listeners immediately after suite instantiation and prior to invoking suite execution routines.
- **R-BMK-003** MUST: Extract cycle target metrics through the event target property on the event object to maintain decoupled telemetry reporting.
- **R-BMK-004** MUST: Enforce defensive programming inside cycle event callbacks to prevent unhandled runtime errors during reporting.

### Verify

```bash
# Discover the repository benchmark script defined in the dependency manifest and execute it to verify suite cycle output.
# Inspect benchmark suite definitions to ensure test lambdas do not contain standard input and output or logging statements.
```

**Accept when:**
- Benchmark suites execute and emit cycle events reporting target completion without throwing unhandled exceptions.
- All benchmark suites register cycle event listeners via the on method and exclude logging logic from add test lambdas.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>