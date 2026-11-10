---
version: 2
name: cross-cutting-schema-engine-variants-delegate-input-6962
description: "Adoption of Shared Core Library Module for Schema Engine Variants: Schema Engine Variants Delegate Input Validation"
metadata:
  actual:
    adr_id: 69629eac-be8b-4c7e-aeff-0723058dda4e
    status: accepted
    candidate_group_id: 138011fb-83e8-4014-9ddd-f54efb32a93b
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Adoption of Shared Core Library Module for Schema Engine Variants: Schema Engine Variants Delegate Input Validation

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all schema engine variants requiring shared parsing, registry lookup, or validation logic, and modules implementing schema validation contracts and instance registries.

### Rules

- **R-SEV-001** SHOULD: Schema engine variants SHOULD delegate input validation and execution handling to shared core verification primitives through safeParse methods.
- **R-SEV-002** MANDATORY: Developers MUST derive tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-SEV-003** MANDATORY: Before writing code that uses a versioned library, developers MUST execute the lock-version grounding procedure in order: find dependency manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for the exact version, confirm every API/class/function exists, and re-run per dependency at point of use.
- **R-SEV-004** MANDATORY: Schema variant implementations MUST verify that interactions with core.globalRegistry properly handle type casting and instance retrieval across execution contexts.
- **R-SEV-005** MANDATORY: When extending schema parsing capabilities, developers MUST evaluate whether new validation checks belong in the shared core module or variant-specific extensions.

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
Claude Code MUST NOT skip or defer verification. Verified by continuous integration automated test suites, static module dependency analysis and import boundary linters, and peer code reviews on all schema engine pull requests.
</enforcement>