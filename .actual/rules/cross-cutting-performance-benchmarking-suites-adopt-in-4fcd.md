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
- **R-META-002** MUST: Follow the DISCOVERY POLICY (MANDATORY): omit all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.
- **R-META-003** MUST: Follow LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, find the dependency manifest, identify the build tool, inspect the repository lock or resolution artifact for the exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run per dependency at point of use.
- **R-META-004** MUST: Import the internal metabench module to structure benchmark cases, separating benchmark setup logic from timed iteration blocks.
- **R-META-005** MUST: Maintain auxiliary utility functions in dedicated utility modules while delegating all measurement harness coordination exclusively to the metabench module.

### Verify

```bash
# Discover the repository configuration and execute the designated benchmark verification script to validate benchmark suite execution.
# Discover and run the project static type-checking and linting scripts to verify compliance with internal module import conventions.
```

**Accept when:**
- All benchmark suites execute successfully through the metabench harness without execution errors.
- Benchmark suite definitions adhere to module import constraints and static type validation passes across all benchmark modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration and code review inspection.
</enforcement>