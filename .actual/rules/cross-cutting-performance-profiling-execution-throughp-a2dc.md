---
version: 2
name: cross-cutting-performance-profiling-execution-throughp-a2dc
description: "Benchmark Library Adoption for Schema Performance Evaluation: Performance Profiling Execution Throughput Measurement Schema"
metadata:
  actual:
    adr_id: a2dce7a2-bf3b-4313-a618-6393e79edc7d
    status: accepted
    candidate_group_id: f25aea77-f01a-48e5-8bc3-2e219c7a9c40
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Library Adoption for Schema Performance Evaluation: Performance Profiling Execution Throughput Measurement Schema

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for performance evaluation and throughput profiling of schema parsing and validation functions.

### Rules

- **R-SCH-001** MUST: Performance profiling and execution throughput measurement for schema validation modules MUST use the benchmark suite API to construct standardized execution cases.

### Verify

```bash
# Discover the performance test script declared in the repository dependency manifest and execute it using the project-designated task runner.
# Inspect the repository task configuration to locate and trigger the benchmark suite execution workflow.
```

**Accept when:**
- All benchmark test suites execute to completion through their registered cycle event handlers without uncaught exceptions.
- Validation parse operations within benchmark cases accurately reflect real-world payload shapes and error conditions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated performance validation workflows triggered during release verification phases and peer code review.
</enforcement>