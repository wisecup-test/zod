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

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-MB-001** MAY: Auxiliary benchmark utility modules MAY be utilized alongside the metabench module exclusively for test data initialization and setup preparation.

### Verify

```bash
# Discover the repository configuration and execute the designated benchmark verification script
# Discover and run the project static type-checking and linting scripts to verify compliance
```

**Accept when:**
- All benchmark suites execute successfully through the metabench harness without execution errors.
- Benchmark suite definitions adhere to module import constraints and static type validation passes across all benchmark modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration and code review inspection enforce exclusive use of the metabench harness.
</enforcement>