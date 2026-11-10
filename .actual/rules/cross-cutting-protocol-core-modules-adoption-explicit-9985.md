---
version: 2
name: cross-cutting-protocol-core-modules-adoption-explicit-9985
description: "node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Before Integrating Updating Dependencies That Interact"
metadata:
  actual:
    adr_id: 9985f9fb-d1b5-4ad8-bc72-151c20d363b9
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

# node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Before Integrating Updating Dependencies That Interact

Scope: applies to `scripts/**`, `vitest.compile.config.ts`, `vitest.config.ts`, `vitest.root.mjs`.

These rules are ALWAYS ACTIVE for all configuration files, automation scripts, verification scripts, and internal modules requiring core system utilities or interacting with runtime core module interfaces.

### Rules

- **R-NODE-001** MUST: Before integrating or updating dependencies that interact with runtime core module interfaces, engineers MUST inspect the project lock artifact to resolve and verify the exact locked version of the runtime and tooling dependencies against official reference documentation.
- **R-NODE-002** MUST: Use explicit protocol-prefixed module specifiers for all runtime core utility modules (such as filesystem, path, and URL capabilities) to prevent dependency shadowing and namespace ambiguity.
- **R-NODE-003** MUST: Ensure all execution runtimes and build tools conform to the resolved versions specified in the repository lock artifact and natively support protocol-prefixed module resolution.

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