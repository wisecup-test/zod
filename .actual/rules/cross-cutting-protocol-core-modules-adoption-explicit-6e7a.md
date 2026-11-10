---
version: 2
name: cross-cutting-protocol-core-modules-adoption-explicit-6e7a
description: "node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Imports Runtime Core Utility Modules Path"
metadata:
  actual:
    adr_id: 6e7a518e-14ac-40fd-9ef2-32eef64f6f2b
    status: accepted
    candidate_group_id: b221aea1-37c8-4893-8cb2-d3c57617eb2f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
      - vitest.compile.config.ts
      - vitest.config.ts
      - vitest.root.mjs
---

# node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Imports Runtime Core Utility Modules Path

Scope: applies to `scripts/**`, `vitest.compile.config.ts`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-NODE-001** MUST: All imports of runtime core utility modules for path manipulation, filesystem access, and URL resolution MUST declare the explicit protocol prefix rather than bare module specifiers.

### Verify

```bash
# Discover and run the repository linter to verify that no bare imports of runtime core modules exist in source or configuration files.
# Discover and run the repository test and type-checking scripts to verify successful resolution of all protocol-prefixed module imports.
```

**Accept when:**
- Static analysis and linting pass with zero violations of core module import prefix rules.
- All test suites and configuration modules execute and resolve runtime core utilities without resolution errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>