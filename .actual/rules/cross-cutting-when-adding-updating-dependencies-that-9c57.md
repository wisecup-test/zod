---
version: 2
name: cross-cutting-when-adding-updating-dependencies-that-9c57
description: "Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: When Adding Updating Dependencies That Interact"
metadata:
  actual:
    adr_id: 9c571fba-4f00-47c8-a677-ebf1437dbba4
    status: accepted
    candidate_group_id: be88ca21-c354-4c2a-953c-43d58c347707
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/resolution/**
      - scripts/**
      - vitest.config.ts
      - vitest.root.mjs
---

# Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: When Adding Updating Dependencies That Interact

Scope: applies to `packages/resolution/**`, `scripts/**`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** MUST: When adding or updating dependencies that interact with runtime core modules, the consumer MUST discover the repository lock artifact and verify resolved versions against the dependency manifest before implementing changes.
- **R-CORE-002** MUST: Import built-in runtime capabilities using explicit `node:` protocol prefixes to eliminate module resolution ambiguity.

### Verify

```bash
# Discover the project's automated verification script from the dependency manifest and run the linter
# Discover and execute the project's test suite to verify module resolution succeeds
```

**Accept when:**
- All workspace modules and scripts import core Node.js runtime facilities exclusively using the node: protocol namespace prefix.
- Static analysis and automated lint checks verify zero un-prefixed standard library module specifiers exist across the codebase.
- Test suites and build verification scripts execute without module resolution ambiguities or warnings.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated code linting rules and CI checks enforce protocol prefixes on runtime core imports.
</enforcement>