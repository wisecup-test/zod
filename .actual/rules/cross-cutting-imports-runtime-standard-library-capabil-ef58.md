---
version: 2
name: cross-cutting-imports-runtime-standard-library-capabil-ef58
description: "Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: Imports Runtime Standard Library Capabilities Use"
metadata:
  actual:
    adr_id: ef584b97-1bd6-41f4-a8ba-a265ae698ff5
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

# Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: Imports Runtime Standard Library Capabilities Use

Scope: applies to `packages/resolution/**`, `scripts/**`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** MUST: All imports of runtime standard library capabilities MUST use explicit protocol-prefixed module specifiers.

### Verify

```bash
# Run the project's linter or static analysis check to verify no un-prefixed core imports exist
# (Discover the exact command from package.json scripts)
npm run lint

# Execute the project's test suite to ensure module resolution succeeds
npm test
```

**Accept when:**
- All workspace modules and scripts import core Node.js runtime facilities exclusively using the node: protocol namespace prefix.
- Static analysis and automated lint checks verify zero un-prefixed standard library module specifiers exist across the codebase.
- Test suites and build verification scripts execute without module resolution ambiguities or warnings.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>