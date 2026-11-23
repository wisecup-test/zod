---
version: 2
name: cross-cutting-developers-not-use-prefixed-bare-341c
description: "Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: Developers Not Use Prefixed Bare Specifiers"
metadata:
  actual:
    adr_id: 341ca0eb-bcc9-4ce2-9a29-3aba58c960e7
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

# Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: Developers Not Use Prefixed Bare Specifiers

Scope: applies to `packages/resolution/**`, `scripts/**`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for:
- All TypeScript and JavaScript source files, maintenance scripts, and runner configurations that reference runtime core modules.

### Rules

- **R-LM-001** MUST_NOT: Developers MUST NOT use un-prefixed bare specifiers when importing built-in runtime standard library modules.

### Verify

- Discover the project's automated verification script from the dependency manifest and run the linter to ensure no un-prefixed core imports exist.
- Discover and execute the project's test suite to verify module resolution succeeds across all configurations.

**Accept when:**

- All workspace modules and scripts import core Node.js runtime facilities exclusively using the node: protocol namespace prefix.
- Static analysis and automated lint checks verify zero un-prefixed standard library module specifiers exist across the codebase.
- Test suites and build verification scripts execute without module resolution ambiguities or warnings.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated code linting rules configured to enforce protocol prefixes on runtime core imports.
- Verified by: Continuous integration verification runs across all configuration files and utility scripts.
- Violation handling: Pull requests containing un-prefixed core module specifiers fail automated linting and must be updated before merging.
- Exception process: Exceptions require architectural review and must document specific legacy platform constraints necessitating bare module specifiers.
</enforcement>
