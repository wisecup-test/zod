---
version: 2
name: cross-cutting-schema-engine-implementations-consume-sh-9fcb
description: "Adoption of Shared Core Library Module for Schema Engine Variants: Schema Engine Implementations Consume Shared Validation"
metadata:
  actual:
    adr_id: 9fcba4de-ba94-44fd-aed5-16c35b5229e1
    status: accepted
    candidate_group_id: 138011fb-83e8-4014-9ddd-f54efb32a93b
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Adoption of Shared Core Library Module for Schema Engine Variants: Schema Engine Implementations Consume Shared Validation

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for schema engine variant definitions and modules implementing schema validation contracts and instance registries.

### Rules

- **R-SCH-001** MUST: Schema engine implementations MUST consume shared validation checks, regular expressions, and registry primitives exclusively through the internal shared core module.

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