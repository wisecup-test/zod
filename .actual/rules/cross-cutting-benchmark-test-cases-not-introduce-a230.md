---
version: 2
name: cross-cutting-benchmark-test-cases-not-introduce-a230
description: "Benchmark Library Adoption for Schema Performance Evaluation: Benchmark Test Cases Not Introduce External"
metadata:
  actual:
    adr_id: a2304bd5-014a-4eeb-b057-73bee34e01e4
    status: accepted
    candidate_group_id: f25aea77-f01a-48e5-8bc3-2e219c7a9c40
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Library Adoption for Schema Performance Evaluation: Benchmark Test Cases Not Introduce External

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for:
- Performance evaluation and throughput profiling of schema parsing and validation functions.
- Regression analysis of core primitive and composite data structure parsers.

### Rules

- **R-LM-001** MUST_NOT: Benchmark test cases MUST NOT introduce external network operations, disk input-output, or unmanaged asynchronous side effects into synchronous parsing cycles.

### Verify

- Discover the performance test script declared in the repository dependency manifest and execute it using the project-designated task runner.
- Inspect the repository task configuration to locate and trigger the benchmark suite execution workflow.

**Accept when:**

- All benchmark test suites execute to completion through their registered cycle event handlers without uncaught exceptions.
- Validation parse operations within benchmark cases accurately reflect real-world payload shapes and error conditions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated performance validation workflows triggered during release verification phases.
- Verified by: Peer code review verifying that schema additions include corresponding benchmark coverage.
- Violation handling: Pull requests introducing unbenchmarked core parsing alterations or ad-hoc timing loops are blocked during review.
- Violation handling: Benchmark suites failing cycle execution or throwing unhandled errors require immediate remediation prior to merge.
- Exception process: Submit an architectural exception request detailing why standardized benchmarking cannot be applied to the specific schema validation path.
- Exception process: Secure approval from the performance engineering group and document the alternative evaluation methodology in repository documentation.
</enforcement>
