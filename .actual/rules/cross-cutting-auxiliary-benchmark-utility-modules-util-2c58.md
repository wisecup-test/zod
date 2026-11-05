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

These rules are ALWAYS ACTIVE for performance benchmarking suites, micro-benchmark test cases, and execution harness orchestration within the repository.

### Rules

- **R-META-001** MAY: Auxiliary benchmark utility modules MAY be utilized alongside the metabench module exclusively for test data initialization and setup preparation.
- **R-META-002** MANDATORY: Import the internal metabench module to structure benchmark cases, separating benchmark setup logic from timed iteration blocks.
- **R-META-003** MANDATORY: Maintain auxiliary utility functions in dedicated utility modules while delegating all measurement harness coordination exclusively to the metabench module.
- **R-META-004** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, find the dependency manifest, identify the build tool, inspect the repository lock or resolution artifact to determine the exact resolved version, look up official documentation for that exact version, and confirm every API/class/function exists before using it.

### Verify

```bash
# Discover and execute the designated benchmark verification script to validate benchmark suite execution
# Discover and run the project static type-checking and linting scripts to verify compliance with internal module import conventions
```

**Accept when:**
- All benchmark suites execute successfully through the metabench harness without execution errors.
- Benchmark suite definitions adhere to module import constraints and static type validation passes across all benchmark modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is enforced via automated continuous integration pipeline running repository benchmark validation scripts and code review inspection ensuring exclusive use of the metabench harness.
</enforcement>