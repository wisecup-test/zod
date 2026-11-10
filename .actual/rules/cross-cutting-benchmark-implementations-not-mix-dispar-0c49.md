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

These rules are ALWAYS ACTIVE for validation routines, schema parsing modules, primitive evaluation routines undergoing performance evaluation, and automated benchmark execution harnesses and regression measurement suites.

### Rules

- **R-BENCH-001** MUST_NOT: Benchmark implementations MUST NOT mix disparate schema workloads into a single suite without isolating comparative baseline evaluations.
- **R-BENCH-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-BENCH-003** MANDATORY: Before writing code that uses a versioned library, execute lock-version grounding in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run per dependency at point of use for version-sensitive behavior.

### Verify

```bash
echo "Discover and execute project benchmark verification scripts from configuration artifacts"
```

**Accept when:**
- All benchmark suites complete execution cycles without unhandled exceptions.
- Cycle event listeners log target operations per second for all registered validation scenarios.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>