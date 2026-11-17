---
version: 2
name: cross-cutting-benchmark-suites-testing-negative-invali-9a07
description: "Adoption of benchmark Library for Performance Measurement Suites: Benchmark Suites Testing Negative Invalid Input"
metadata:
  actual:
    adr_id: 9a077601-6286-4a5e-b5e5-a1a0ddbe1d43
    status: accepted
    candidate_group_id: a40953fe-dded-4098-9e8e-51ebfac73e1a
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Adoption of benchmark Library for Performance Measurement Suites: Benchmark Suites Testing Negative Invalid Input

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for validation routines, schema parsing modules, and primitive evaluation routines undergoing performance evaluation, and automated benchmark execution harnesses and regression measurement suites.

### Rules

- **R-BENCH-001** MUST: Benchmark suites testing negative or invalid input conditions MUST encapsulate failing calls within error handling blocks to prevent execution interruption during sample cycles.

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