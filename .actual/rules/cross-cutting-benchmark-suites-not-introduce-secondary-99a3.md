---
version: 2
name: cross-cutting-benchmark-suites-not-introduce-secondary-99a3
description: "Adoption of metabench Module for Benchmark Suite Execution: Benchmark Suites Not Introduce Secondary Hoc"
metadata:
  actual:
    adr_id: 99a3b135-4d52-45a3-b758-77d7182de21f
    status: accepted
    candidate_group_id: b9904703-b2ce-4b3d-91ac-98c45f380b73
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
---

# Adoption of metabench Module for Benchmark Suite Execution: Benchmark Suites Not Introduce Secondary Hoc

Scope: applies to `packages/bench/**`.

These rules are ALWAYS ACTIVE for performance benchmarking suites, micro-benchmark test cases, and execution harness orchestration within the repository.

### Rules

- **R-METABENCH-001** MUST_NOT: Benchmark suites MUST NOT introduce secondary or ad-hoc benchmarking runner frameworks for suite execution outside of the standardized metabench module.

### Verify

```bash
# Discover and execute the designated benchmark verification script
# Discover and run static type-checking and linting scripts to verify compliance with internal module import conventions
```

**Accept when:**
- All benchmark suites execute successfully through the metabench harness without execution errors.
- Benchmark suite definitions adhere to module import constraints and static type validation passes across all benchmark modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline runs repository benchmark validation scripts and code review inspects benchmark suites to ensure exclusive use of the metabench harness.
</enforcement>