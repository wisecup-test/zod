---
version: 2
name: cross-cutting-modules-not-import-monolithic-validation-f580
description: "Adoption of zod/mini for Modular Schema Definition and Input Validation: Modules Not Import Monolithic Validation Namespaces"
metadata:
  actual:
    adr_id: f5807871-334d-4e9c-a14b-681b574e30b9
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

# Adoption of zod/mini for Modular Schema Definition and Input Validation: Modules Not Import Monolithic Validation Namespaces

Scope: applies to `packages/bench/**`, `packages/resolution/src/**`, `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all runtime input parsing, schema definitions, and payload verification in shared and client-facing packages.

### Rules

- **R-VAL-001** MUST_NOT: Modules MUST NOT import monolithic validation namespaces where modular schema primitives fulfill the validation requirements.

### Verify

```bash
# Discover and run the repository verification scripts that validate module imports and runtime parsing test suites.
# Inspect module resolution outputs to verify that only modular validation primitives are bundled into target artifacts.
```

**Accept when:**
- All schema validation implementations execute runtime parsing through the designated modular validation entry point.
- Repository verification scripts confirm schema validation tests pass without unapproved monolithic validator imports.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>