---
version: 2
name: cross-cutting-engineers-verify-repository-dependency-l-be88
description: "Adoption of benchmark Library for Performance Measurement Suites: Engineers Verify Repository Dependency Lock Artifact"
metadata:
  actual:
    adr_id: be883fdc-2bf8-49e0-89a9-27d6a71fd598
    status: accepted
    candidate_group_id: a40953fe-dded-4098-9e8e-51ebfac73e1a
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Adoption of benchmark Library for Performance Measurement Suites: Engineers Verify Repository Dependency Lock Artifact

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for validation routines, schema parsing modules, primitive evaluation routines undergoing performance evaluation, and automated benchmark execution harnesses and regression measurement suites.

### Rules

- **R-ADR-001** MUST: Engineers MUST verify the repository dependency lock artifact to determine the exact resolved dependency version prior to implementing or updating benchmark suite integrations.

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