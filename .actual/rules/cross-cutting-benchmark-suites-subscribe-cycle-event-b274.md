---
version: 2
name: cross-cutting-benchmark-suites-subscribe-cycle-event-b274
description: "Benchmark Library Adoption for Schema Performance Evaluation: Benchmark Suites Subscribe Cycle Event Listener"
metadata:
  actual:
    adr_id: b2741759-18f3-471e-9d7c-3eeaa3a13ac2
    status: accepted
    candidate_group_id: f25aea77-f01a-48e5-8bc3-2e219c7a9c40
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Library Adoption for Schema Performance Evaluation: Benchmark Suites Subscribe Cycle Event Listener

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for performance evaluation and throughput profiling of schema parsing and validation functions, and regression analysis of core primitive and composite data structure parsers.

### Rules

- **R-BENCH-001** SHOULD: Benchmark suites SHOULD subscribe to the cycle event using the on listener to record target performance metrics upon completion of each scenario evaluation.
- **R-BENCH-002** MANDATORY: Discover the performance test script declared in the repository dependency manifest and execute it using the project-designated task runner, and inspect the repository task configuration to locate and trigger the benchmark suite execution workflow.
- **R-BENCH-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find the dependency manifest in the repo, identify the build tool, inspect the repository lock or resolution artifact to determine the exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version's documentation, and re-run steps 3-5 per dependency at point of use for version-sensitive behavior.
- **R-BENCH-004** MANDATORY: Ensure test payloads represent both minimal and fully populated data structures to measure parsing boundaries accurately, and keep benchmark scenario definitions isolated to avoid cross-suite state contamination during cycle execution.

### Verify

```bash
# Discover and execute the performance test script declared in the repository dependency manifest using the project-designated task runner
# Inspect repository task configuration to locate and trigger the benchmark suite execution workflow
```

**Accept when:**
- All benchmark test suites execute to completion through their registered cycle event handlers without uncaught exceptions.
- Validation parse operations within benchmark cases accurately reflect real-world payload shapes and error conditions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated performance validation workflows, peer code reviews, and architectural exception processes enforce these rules.
</enforcement>