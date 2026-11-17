---
version: 2
name: cross-cutting-performance-benchmark-modules-construct-3362
description: "Adoption of benchmark Library for Performance Measurement Suites: Performance Benchmark Modules Construct Benchmarking Suites"
metadata:
  actual:
    adr_id: 3362d22d-9ccb-41f4-916c-e2cb7f498d74
    status: accepted
    candidate_group_id: a40953fe-dded-4098-9e8e-51ebfac73e1a
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Adoption of benchmark Library for Performance Measurement Suites: Performance Benchmark Modules Construct Benchmarking Suites

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for validation routines, schema parsing modules, primitive evaluation routines undergoing performance evaluation, and automated benchmark execution harnesses and regression measurement suites.

### Rules

- **R-PERF-001** MUST: Performance benchmark modules MUST construct benchmarking suites exclusively through the benchmark library to standardize statistical sampling and cycle metrics across validation routines.

### Verify

```bash
echo "Discover and execute project benchmark verification scripts from configuration artifacts"
```

**Accept when:**
- All benchmark suites complete execution cycles without unhandled exceptions.
- Cycle event listeners log target operations per second for all registered validation scenarios.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>