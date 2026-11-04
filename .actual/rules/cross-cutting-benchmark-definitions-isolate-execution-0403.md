---
version: 2
name: cross-cutting-benchmark-definitions-isolate-execution-0403
description: "Adoption of metabench Module for Benchmark Suite Execution: Benchmark Definitions Isolate Execution Iterations Timing"
metadata:
  actual:
    adr_id: 0403b551-69c3-4a30-a0cb-9f8df8753d4e
    status: accepted
    candidate_group_id: b9904703-b2ce-4b3d-91ac-98c45f380b73
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
---

# Adoption of metabench Module for Benchmark Suite Execution: Benchmark Definitions Isolate Execution Iterations Timing

Scope: applies to `packages/bench/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-META-001** SHOULD: Benchmark definitions SHOULD isolate execution iterations and timing collection through the standardized harness lifecycle provided by the metabench module.

### Verify

```bash
# Discover the repository configuration and execute the designated benchmark verification script to validate benchmark suite execution.
# Discover and run the project static type-checking and linting scripts to verify compliance with internal module import conventions.
```

**Accept when:**
- All benchmark suites execute successfully through the metabench harness without execution errors.
- Benchmark suite definitions adhere to module import constraints and static type validation passes across all benchmark modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>