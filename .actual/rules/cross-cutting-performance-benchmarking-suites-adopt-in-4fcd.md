---
version: 2
name: cross-cutting-performance-benchmarking-suites-adopt-in-4fcd
description: "Adoption of metabench Module for Benchmark Suite Execution: Performance Benchmarking Suites Adopt Internal Metabench"
metadata:
  actual:
    adr_id: 4fcd575f-fd26-4ed7-ab9b-f7b87fec40e8
    status: accepted
    candidate_group_id: b9904703-b2ce-4b3d-91ac-98c45f380b73
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
---

# Adoption of metabench Module for Benchmark Suite Execution: Performance Benchmarking Suites Adopt Internal Metabench

Scope: applies to `packages/bench/**`.

These rules are ALWAYS ACTIVE for all performance benchmarking suites and micro-benchmark test cases within the repository.

### Rules

- **R-META-001** MUST: All performance benchmarking suites MUST adopt the internal metabench module as the authoritative harness for executing benchmark cases and collecting timing measurements.
- **R-META-002** MANDATORY: Execute the lock-version grounding process (discover manifest, build tool, and lock/resolution artifact; inspect official docs for exact resolved version) before writing code that uses a versioned library.
- **R-META-003** MANDATORY: Discover repository configuration and execute the designated benchmark verification script, as well as static type-checking and linting scripts, to validate benchmark suite execution and compliance with internal module import conventions.

### Verify

```bash
# Discover and execute project benchmarking suites via the internal harness
# (Command to be derived from the project repository configuration)

# Discover and run static type-checking and linting scripts
# (Command to be derived from the project repository configuration)
```

**Accept when:**
- All benchmark suites execute successfully through the metabench harness without execution errors.
- Benchmark suite definitions adhere to module import constraints and static type validation passes across all benchmark modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>