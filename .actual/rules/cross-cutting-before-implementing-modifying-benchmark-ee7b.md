---
version: 2
name: cross-cutting-before-implementing-modifying-benchmark-ee7b
description: "Benchmark Library Adoption for Schema Performance Evaluation: Before Implementing Modifying Benchmark Suites Engineers"
metadata:
  actual:
    adr_id: ee7b2879-0b5a-4553-85b3-bebdb81b8bc0
    status: accepted
    candidate_group_id: f25aea77-f01a-48e5-8bc3-2e219c7a9c40
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Library Adoption for Schema Performance Evaluation: Before Implementing Modifying Benchmark Suites Engineers

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for performance evaluation and throughput profiling of schema parsing and validation functions, and regression analysis of core primitive and composite data structure parsers.

### Rules

- **R-BENCH-001** MUST: Before implementing or modifying benchmark suites, engineers MUST inspect the repository lock artifact to determine the exact resolved version of the benchmark library and verify API compatibility against authoritative documentation.

### Verify

```bash
# Discover the performance test script declared in the repository dependency manifest and execute it using the project-designated task runner.
# Inspect the repository task configuration to locate and trigger the benchmark suite execution workflow.
```

**Accept when:**
- All benchmark test suites execute to completion through their registered cycle event handlers without uncaught exceptions.
- Validation parse operations within benchmark cases accurately reflect real-world payload shapes and error conditions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>