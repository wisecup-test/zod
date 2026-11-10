---
version: 2
name: cross-cutting-benchmark-suites-attach-cycle-listeners-a110
description: "Adoption of benchmark Library for Performance Measurement Suites: Benchmark Suites Attach Cycle Listeners Via"
metadata:
  actual:
    adr_id: a110d8e6-6c89-42d7-86eb-fe5c5fb350b8
    status: accepted
    candidate_group_id: a40953fe-dded-4098-9e8e-51ebfac73e1a
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Adoption of benchmark Library for Performance Measurement Suites: Benchmark Suites Attach Cycle Listeners Via

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for validation routines, schema parsing modules, primitive evaluation routines undergoing performance evaluation, and automated benchmark execution harnesses and regression measurement suites.

### Rules

- **R-BENCH-001** SHOULD: Benchmark suites SHOULD attach cycle listeners via the `on` method with the cycle event parameter to record standardized per-scenario throughput diagnostics.

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