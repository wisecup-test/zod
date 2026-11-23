---
version: 2
name: cross-cutting-auxiliary-benchmark-utility-modules-util-2c58
description: "Adoption of metabench Module for Benchmark Suite Execution: Auxiliary Benchmark Utility Modules Utilized Alongside"
metadata:
  actual:
    adr_id: 2c58ccd7-b421-4480-be26-24c342badc14
    status: accepted
    candidate_group_id: b9904703-b2ce-4b3d-91ac-98c45f380b73
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
---

# Adoption of metabench Module for Benchmark Suite Execution: Auxiliary Benchmark Utility Modules Utilized Alongside

Scope: applies to `packages/bench/**`.

These rules are ALWAYS ACTIVE for:
- Performance benchmarking suites and micro-benchmark test cases within the repository.
- Execution harness orchestration and performance measurement cycles.

### Rules

- **R-LM-001** MAY: Auxiliary benchmark utility modules MAY be utilized alongside the metabench module exclusively for test data initialization and setup preparation.

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
