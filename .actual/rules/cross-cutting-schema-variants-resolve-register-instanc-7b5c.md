---
version: 2
name: cross-cutting-schema-variants-resolve-register-instanc-7b5c
description: "Adoption of Shared Core Library Module for Schema Engine Variants: Schema Variants Resolve Register Instances Through"
metadata:
  actual:
    adr_id: 7b5c7d5c-3e46-409b-a486-d5c6346a535f
    status: accepted
    candidate_group_id: 138011fb-83e8-4014-9ddd-f54efb32a93b
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Adoption of Shared Core Library Module for Schema Engine Variants: Schema Variants Resolve Register Instances Through

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all schema engine variant definitions, validation modules, and instance registry implementations requiring shared parsing, registry lookup, or validation logic.

### Rules

- **R-CORE-001** MUST: Schema variants MUST resolve and register schema instances through core.globalRegistry to ensure cross-variant schema lookup compatibility.

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
Claude Code MUST NOT skip or defer verification. All pull requests that duplicate core parsing logic or bypass the shared core module are blocked from merging.
</enforcement>