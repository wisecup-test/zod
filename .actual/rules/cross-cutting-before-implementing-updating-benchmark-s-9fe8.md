---
version: 2
name: cross-cutting-before-implementing-updating-benchmark-s-9fe8
description: "Adoption of metabench Module for Benchmark Suite Execution: Before Implementing Updating Benchmark Suites That"
metadata:
  actual:
    adr_id: 9fe8f0f7-5ef8-4fc7-bd82-ba7f34f4630d
    status: accepted
    candidate_group_id: b9904703-b2ce-4b3d-91ac-98c45f380b73
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
---

# Adoption of metabench Module for Benchmark Suite Execution: Before Implementing Updating Benchmark Suites That

Scope: applies to `packages/bench/**`.

These rules are ALWAYS ACTIVE for:
- Performance benchmarking suites and micro-benchmark test cases within the repository.
- Execution harness orchestration and performance measurement cycles.

### Rules

- **R-LM-001** MUST: Before implementing or updating benchmark suites that rely on dependencies, consumers MUST discover the repository dependency manifest and inspect the authoritative lock artifact to verify resolved dependency versions against official documentation.

### Verify

- Discover the repository configuration and execute the designated benchmark verification script to validate benchmark suite execution.
- Discover and run the project static type-checking and linting scripts to verify compliance with internal module import conventions.

**Accept when:**

- All benchmark suites execute successfully through the metabench harness without execution errors.
- Benchmark suite definitions adhere to module import constraints and static type validation passes across all benchmark modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline running repository benchmark validation scripts.
- Verified by: Code review inspection of benchmark suites to ensure exclusive use of the metabench harness.
- Violation handling: Pull requests introducing ad-hoc benchmark runners or bypassing the metabench harness will fail code review and automated checks.
- Exception process: Exceptions must be requested through an architecture review proposal detailing why the metabench module cannot support the specific benchmark requirement.
</enforcement>
