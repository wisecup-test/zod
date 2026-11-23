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

These rules are ALWAYS ACTIVE for:
- All repository configuration files requiring core system utilities
- All automation and verification scripts interfacing with filesystem, path, or URL capabilities
- All internal modules relying on runtime platform interfaces

### Rules

- **R-LM-001** MUST: Before integrating or updating dependencies that interact with runtime core module interfaces, engineers MUST inspect the project lock artifact to resolve and verify the exact locked version of the runtime and tooling dependencies against official reference documentation.

### Verify

- Discover and run the repository linter to verify that no bare imports of runtime core modules exist in source or configuration files.
- Discover and run the repository test and type-checking scripts to verify successful resolution of all protocol-prefixed module imports.

**Accept when:**

- Static analysis and linting pass with zero violations of core module import prefix rules.
- All test suites and configuration modules execute and resolve runtime core utilities without resolution errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration lint checks inspecting import specifiers
- Verified by: Code review validation for all new configuration files and utility scripts
- Violation handling: Pull requests containing bare specifiers for runtime core modules are blocked by automated continuous integration
- Violation handling: Violations must be updated to use the explicit protocol prefix before merge approval
- Exception process: Exceptions for legacy compatibility require written justification and approval from the lead architecture maintainers.
</enforcement>
