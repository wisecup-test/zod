---
version: 2
name: cross-cutting-modules-requiring-schema-definition-runt-16be
description: "Adoption of zod/mini for Modular Schema Definition and Input Validation: Modules Requiring Schema Definition Runtime Input"
metadata:
  actual:
    adr_id: 16be4ea5-22ca-4902-a7df-d2b65ae63bbb
    status: accepted
    candidate_group_id: 6019c7a4-9a84-4a99-a2a2-7b9ec4210fe7
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
      - packages/resolution/src/**
      - packages/treeshake/**
---

# Adoption of zod/mini for Modular Schema Definition and Input Validation: Modules Requiring Schema Definition Runtime Input

Scope: applies to `packages/bench/**`, `packages/resolution/src/**`, `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: Modules requiring schema definition and runtime input validation MUST import and utilize the zod/mini entry point.

### Verify

```bash
# Discover and run repository verification scripts that validate module imports and runtime parsing test suites.
# Inspect module resolution outputs to verify that only modular validation primitives are bundled into target artifacts.
```

**Accept when:**
- All schema validation implementations execute runtime parsing through the designated modular validation entry point.
- Repository verification scripts confirm schema validation tests pass without unapproved monolithic validator imports.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis, module import inspection, and code review.
</enforcement>