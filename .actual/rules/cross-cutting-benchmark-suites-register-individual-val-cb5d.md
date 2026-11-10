---
version: 2
name: cross-cutting-benchmark-suites-register-individual-val-cb5d
description: "Benchmark Library Adoption for Schema Performance Evaluation: Benchmark Suites Register Individual Validation Scenarios"
metadata:
  actual:
    adr_id: cb5df181-b80e-40d2-8b80-f49c3c319b5d
    status: accepted
    candidate_group_id: f25aea77-f01a-48e5-8bc3-2e219c7a9c40
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Library Adoption for Schema Performance Evaluation: Benchmark Suites Register Individual Validation Scenarios

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for performance evaluation and throughput profiling of schema parsing and validation functions, and regression analysis of core primitive and composite data structure parsers.

### Rules

- **R-SCH-001** MUST: Benchmark suites register individual validation scenarios using the suite add method, separating valid input parsing from invalid input failure paths.

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