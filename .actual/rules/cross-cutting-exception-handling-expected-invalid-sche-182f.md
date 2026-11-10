---
version: 2
name: cross-cutting-exception-handling-expected-invalid-sche-182f
description: "Benchmark Library Adoption for Schema Performance Evaluation: Exception Handling Expected Invalid Schema Inputs"
metadata:
  actual:
    adr_id: 182f4f64-d5e5-4087-be15-9639edbd7b63
    status: accepted
    candidate_group_id: f25aea77-f01a-48e5-8bc3-2e219c7a9c40
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Library Adoption for Schema Performance Evaluation: Exception Handling Expected Invalid Schema Inputs

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for performance evaluation and throughput profiling of schema parsing and validation functions, and regression analysis of core primitive and composite data structure parsers.

### Rules

- **R-SCH-001** MUST: Exception handling for expected invalid schema inputs within benchmark scenarios MUST be contained within localized error-capturing blocks to prevent cycle interruption.

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