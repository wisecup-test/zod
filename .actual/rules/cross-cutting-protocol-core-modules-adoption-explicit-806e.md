---
version: 2
name: cross-cutting-protocol-core-modules-adoption-explicit-806e
description: "node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Source Modules Configuration Units Repository Utility"
metadata:
  actual:
    adr_id: 806ea227-7a7f-4e6a-865c-923690bbb0ad
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

# node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Source Modules Configuration Units Repository Utility

Scope: applies to `scripts/**`, `vitest.compile.config.ts`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for all source modules, configuration units, repository utility scripts, and automation tasks interfacing with runtime core utilities.

### Rules

- **R-NODE-001** MUST_NOT: Source modules, configuration units, and repository utility scripts MUST NOT import runtime core utilities using un-prefixed bare specifiers.

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