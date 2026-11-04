---
version: 2
name: cross-cutting-static-analysis-linter-configurations-co-8eb5
description: "Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: Static Analysis Linter Configurations Configured Automatically"
metadata:
  actual:
    adr_id: 8eb5dbec-7303-49e1-9332-b3739fb92900
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

# Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: Static Analysis Linter Configurations Configured Automatically

Scope: applies to `packages/resolution/**`, `scripts/**`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for all TypeScript and JavaScript source files, maintenance scripts, and runner configurations that reference runtime core modules.

### Rules

- **R-NODE-001** SHOULD: Static analysis and linter configurations SHOULD be configured to automatically enforce and autofix protocol-prefixed module specifiers across all codebase entries.

### Verify

```bash
# Discover the project's automated verification script from the dependency manifest and run the linter
# Example discovery step:
LINT_CMD=$(npm pkg get scripts.lint 2>/dev/null | tr -d '"')
if [ -n "$LINT_CMD" ] && [ "$LINT_CMD" != "null" ]; then
  npm run lint
else
  npx eslint .
fi

# Discover and execute the project's test suite to verify module resolution
TEST_CMD=$(npm pkg get scripts.test 2>/dev/null | tr -d '"')
if [ -n "$TEST_CMD" ] && [ "$TEST_CMD" != "null" ]; then
  npm test
fi
```

**Accept when:**
- All workspace modules and scripts import core Node.js runtime facilities exclusively using the node: protocol namespace prefix.
- Static analysis and automated lint checks verify zero un-prefixed standard library module specifiers exist across the codebase.
- Test suites and build verification scripts execute without module resolution ambiguities or warnings.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests containing un-prefixed core module specifiers fail automated linting and must be updated before merging.
</enforcement>