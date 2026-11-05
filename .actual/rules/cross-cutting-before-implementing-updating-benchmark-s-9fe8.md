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

These rules are ALWAYS ACTIVE for performance benchmarking suites and micro-benchmark test cases within the repository.

### Rules

- **R-META-001** MUST: Before implementing or updating benchmark suites that rely on dependencies, consumers MUST discover the repository dependency manifest and inspect the authoritative lock artifact to verify resolved dependency versions against official documentation.
- **R-META-002** MUST: Import the internal metabench module to structure benchmark cases, separating benchmark setup logic from timed iteration blocks.
- **R-META-003** SHOULD: Maintain auxiliary utility functions in dedicated utility modules while delegating all measurement harness coordination exclusively to the metabench module.

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