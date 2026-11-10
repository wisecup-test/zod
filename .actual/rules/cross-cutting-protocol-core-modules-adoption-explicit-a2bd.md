---
version: 2
name: cross-cutting-protocol-core-modules-adoption-explicit-a2bd
description: "node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Module Path Resolutions Directory Url Derivations"
metadata:
  actual:
    adr_id: a2bd86d1-efc7-4614-b7be-274d2f752f4e
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

# node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Module Path Resolutions Directory Url Derivations

Scope: applies to `scripts/**`, `vitest.compile.config.ts`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for all repository configuration files, automation and verification scripts interfacing with filesystem, path, or URL capabilities, and internal modules relying on runtime platform interfaces.

### Rules

- **R-NODE-001** SHOULD: Module path resolutions and directory URL derivations SHOULD use protocol-prefixed path and URL utilities consistently across all configuration definitions and execution scripts.

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