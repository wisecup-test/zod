---
version: 2
name: cross-cutting-custom-validation-constraints-declared-m-7cca
description: "Adoption of zod/mini for Modular Schema Definition and Input Validation: Custom Validation Constraints Declared Modular Check"
metadata:
  actual:
    adr_id: 7ccaa146-eb38-475f-aef8-37a45cc3d7bb
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

# Adoption of zod/mini for Modular Schema Definition and Input Validation: Custom Validation Constraints Declared Modular Check

Scope: applies to `packages/bench/**`, `packages/resolution/src/**`, `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VAL-001** SHOULD: Custom validation constraints SHOULD be declared using modular check functions attached to base type schemas.
- **R-VAL-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-VAL-003** MANDATORY: Before writing code that uses a versioned library, the consumer MUST execute the lock-version grounding steps in order (find manifest, identify build tool, inspect lock artifact, look up official documentation for that exact version, confirm every API/class/function exists, and re-run per dependency at point of use).

### Verify

```bash
# Discover and run the repository verification scripts that validate module imports and runtime parsing test suites.
# Inspect module resolution outputs to verify that only modular validation primitives are bundled into target artifacts.
```

**Accept when:**
- All schema validation implementations execute runtime parsing through the designated modular validation entry point.
- Repository verification scripts confirm schema validation tests pass without unapproved monolithic validator imports.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and module import inspection in continuous integration workflows verify these rules.
</enforcement>