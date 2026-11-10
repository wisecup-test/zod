---
version: 2
name: cross-cutting-protocol-core-modules-adoption-explicit-2b3c
description: "node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Modules Not Install Third Party Utility"
metadata:
  actual:
    adr_id: 2b3c6789-0e14-475d-b09f-21f52d4ca86d
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

# node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Modules Not Install Third Party Utility

Scope: applies to `scripts/**`, `vitest.compile.config.ts`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-NODE-001** SHOULD_NOT: Modules SHOULD NOT install third-party utility packages to replicate capabilities natively provided by protocol-prefixed runtime core modules unless specialized polyfill requirements exist.

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