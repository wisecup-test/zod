---
version: 2
name: cross-cutting-runtime-input-parsing-executed-through-1ac1
description: "Adoption of zod/mini for Modular Schema Definition and Input Validation: Runtime Input Parsing Executed Through Schema"
metadata:
  actual:
    adr_id: 1ac1e47a-9433-4fdd-a043-d57d25629c09
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

# Adoption of zod/mini for Modular Schema Definition and Input Validation: Runtime Input Parsing Executed Through Schema

Scope: applies to `packages/bench/**`, `packages/resolution/src/**`, `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all runtime input parsing, schema definitions, and payload verification in shared and client-facing packages.

### Rules

- **R-MOD-001** MUST: Runtime input parsing MUST be executed through schema parse invocations rather than ad-hoc unchecked type assertions.

### Verify

```bash
# Discover and run repository verification scripts that validate module imports and runtime parsing test suites
# (Repository-specific verification script execution)
```

**Accept when:**
- All schema validation implementations execute runtime parsing through the designated modular validation entry point.
- Repository verification scripts confirm schema validation tests pass without unapproved monolithic validator imports.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and module import inspection in CI will flag non-modular validation namespaces or direct manual validation assertions as blocking violations.
</enforcement>