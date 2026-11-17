---
version: 2
name: cross-cutting-before-introducing-modifying-versioned-d-77bf
description: "Adoption of Shared Core Library Module for Schema Engine Variants: Before Introducing Modifying Versioned Dependencies Consumer"
metadata:
  actual:
    adr_id: 77bf6989-720d-48d1-b444-e32ae5f3eb94
    status: accepted
    candidate_group_id: 138011fb-83e8-4014-9ddd-f54efb32a93b
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Adoption of Shared Core Library Module for Schema Engine Variants: Before Introducing Modifying Versioned Dependencies Consumer

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for schema engine variant definitions requiring shared parsing, registry lookup, or validation logic, and modules implementing schema validation contracts and instance registries.

### Rules

- **R-SCH-001** MUST: Before introducing or modifying versioned dependencies, the consumer MUST inspect the repository lock or resolution artifact to verify the exact resolved dependency version.

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
Claude Code MUST NOT skip or defer verification. Continuous integration automated test suites, static module dependency analysis, and import boundary linters enforce these rules. Pull requests that duplicate core parsing logic or bypass the shared core module are blocked from merging.
</enforcement>