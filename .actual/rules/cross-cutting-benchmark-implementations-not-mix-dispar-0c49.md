---
version: 2
name: cross-cutting-benchmark-implementations-not-mix-dispar-0c49
description: "Adoption of benchmark Library for Performance Measurement Suites: Benchmark Implementations Not Mix Disparate Schema"
metadata:
  actual:
    adr_id: 0c495181-1545-472c-9907-14c9c44288ba
    status: accepted
    candidate_group_id: a40953fe-dded-4098-9e8e-51ebfac73e1a
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Adoption of benchmark Library for Performance Measurement Suites: Benchmark Implementations Not Mix Disparate Schema

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for:
- Validation routines, schema parsing modules, and primitive evaluation routines undergoing performance evaluation
- Automated benchmark execution harnesses and regression measurement suites

### Rules

- **R-LM-001** MUST_NOT: Benchmark implementations MUST NOT mix disparate schema workloads into a single suite without isolating comparative baseline evaluations.

### Verify

- echo "Discover and execute project benchmark verification scripts from configuration artifacts"

**Accept when:**

- All benchmark suites complete execution cycles without unhandled exceptions.
- Cycle event listeners log target operations per second for all registered validation scenarios.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline execution of benchmark verification targets.
- Verified by: Peer code review for all new schema primitives and parsing performance test cases.
- Violation handling: Pull requests introducing validation primitives without corresponding benchmark coverage are blocked from merging.
- Violation handling: Benchmark execution failures or unhandled cycle errors fail the continuous integration build.
- Exception process: Exceptions require documented architectural justification and explicit sign-off from the technical lead.
</enforcement>
