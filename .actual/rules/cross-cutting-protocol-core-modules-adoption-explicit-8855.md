---
version: 2
name: cross-cutting-protocol-core-modules-adoption-explicit-8855
description: "node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Input Validation Serialization Routines Reading Filesystem"
metadata:
  actual:
    adr_id: 8855787a-2ca9-48d0-8e07-bca1a1ac414e
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

# node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Input Validation Serialization Routines Reading Filesystem

Scope: applies to `scripts/**`, `vitest.compile.config.ts`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for all repository configuration files requiring core system utilities, automation and verification scripts interfacing with filesystem, path, or URL capabilities, and internal modules relying on runtime platform interfaces.

### Rules

- **R-CORE-001** MUST: Input validation and serialization routines reading filesystem contents MUST parse data structures defensively through validated deserialization mechanisms.

### Verify

```bash
# Discover and run the repository linter to verify that no bare imports of runtime core modules exist in source or configuration files.
# Discover and run the repository test and type-checking scripts to verify successful resolution of all protocol-prefixed module imports.
```

**Accept when:**
- Static analysis and linting pass with zero violations of core module import prefix rules.
- All test suites and configuration modules execute and resolve runtime core utilities without resolution errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification by automated continuous integration lint checks inspecting import specifiers and code review validation is mandatory. Pull requests containing bare specifiers for runtime core modules are blocked.
</enforcement>