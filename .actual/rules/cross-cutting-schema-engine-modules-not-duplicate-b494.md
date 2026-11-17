---
version: 2
name: cross-cutting-schema-engine-modules-not-duplicate-b494
description: "Adoption of Shared Core Library Module for Schema Engine Variants: Schema Engine Modules Not Duplicate Internal"
metadata:
  actual:
    adr_id: b4945a74-5663-494d-8a0b-21b878458e2a
    status: accepted
    candidate_group_id: 138011fb-83e8-4014-9ddd-f54efb32a93b
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Adoption of Shared Core Library Module for Schema Engine Variants: Schema Engine Modules Not Duplicate Internal

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all schema engine variants requiring shared parsing, registry lookup, or validation logic, and modules implementing schema validation contracts and instance registries.

### Rules

- **R-CORE-001** MUST_NOT: Schema engine modules MUST_NOT duplicate internal regular expression definitions or core parsing algorithms locally.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify adherence to module import boundaries.
# Discover and execute the project test runner across all schema variant test suites to ensure uniform validation behavior.
# Inspect dependency manifests and resolution artifacts to confirm that dependency version declarations match lock state.
```

**Accept when:**
- All schema variant test suites pass without regressions across validation parsing and execution.
- Static boundary verification confirms schema modules import shared parsing and registry primitives exclusively from the internal core module.
- Registry lookup tests confirm consistent resolution of schema instances through core.globalRegistry across variants.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>