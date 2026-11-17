---
version: 2
name: cross-cutting-lightweight-schema-variants-selectively-5f08
description: "Adoption of Shared Core Library Module for Schema Engine Variants: Lightweight Schema Variants Selectively Omit Optional"
metadata:
  actual:
    adr_id: 5f084c3e-4a2f-4add-bb2e-1131ea41a331
    status: accepted
    candidate_group_id: 138011fb-83e8-4014-9ddd-f54efb32a93b
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Adoption of Shared Core Library Module for Schema Engine Variants: Lightweight Schema Variants Selectively Omit Optional

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for schema engine variant definitions, validation contracts, instance registries, and modules interacting with core execution utilities and global registry operations.

### Rules

- **R-CORE-001** MAY: Lightweight schema variants MAY selectively omit optional core schema processors when their targeted execution profile does not require extended schema transformations.
- **R-CORE-002** MANDATORY: Consumers MUST derive tools, file names, commands, package managers, and version numbers from the project repository.
- **R-CORE-003** MANDATORY: Before writing code that uses a versioned library, execution MUST follow the lock-version grounding order: find manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for exact version, confirm every API/class/function exists, and re-run steps per dependency at point of use.
- **R-CORE-004** MANDATORY: Schema variant implementations must verify that interactions with core.globalRegistry properly handle type casting and instance retrieval across execution contexts.
- **R-CORE-005** MANDATORY: When extending schema parsing capabilities, developers must evaluate whether new validation checks belong in the shared core module or variant-specific extensions.

### Verify

```bash
# Discover and run static analysis and linting scripts to verify adherence to module import boundaries
# Discover and execute project test runner across all schema variant test suites
# Inspect dependency manifests and resolution artifacts to confirm dependency version declarations match lock state
```

**Accept when:**
- All schema variant test suites pass without regressions across validation parsing and execution.
- Static boundary verification confirms schema modules import shared parsing and registry primitives exclusively from the internal core module.
- Registry lookup tests confirm consistent resolution of schema instances through core.globalRegistry across variants.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via continuous integration automated test suites, static module dependency analysis, import boundary linters, and peer code reviews.
</enforcement>