---
version: 2
name: cross-cutting-submodule-exports-expose-only-unified-5439
description: "Zod Shared External Core Module Delegation: Submodule Exports Expose Only Unified Public"
metadata:
  actual:
    adr_id: 54390e1f-ba8b-4ed3-8b4d-0fba4c2a16cf
    status: accepted
    candidate_group_id: a85551aa-2a78-4339-85e4-5099508ef143
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/mini/**
      - src/v4-mini/**
---

# Zod Shared External Core Module Delegation: Submodule Exports Expose Only Unified Public

Scope: applies to `packages/zod/src/mini/**`, `packages/zod/src/v4-mini/**`.

These rules are ALWAYS ACTIVE for all modular and lightweight package entry point exports within the library workspace and internal submodules providing public or semi-public validation surface definitions.

### Rules

- **R-ZOD-001** SHOULD: Submodule exports SHOULD expose only the unified public surface provided by the designated external core module.
- **R-ZOD-002** MANDATORY: Ensure all re-exported symbols from the shared external core module preserve type definitions and parameter constraints identical to the primary library exports.
- **R-ZOD-003** MANDATORY: Structure entry facades as pure re-export boundaries with minimal to zero runtime initialization code.
- **R-ZOD-004** MANDATORY: Execute lock-version grounding in order (manifest -> build tool -> lock/resolution artifact -> version-specific docs -> API existence confirmation) before writing code that uses a versioned library.

### Verify

```bash
# Discover the repository build script from the project manifest and execute the compilation verification task to validate module export compatibility.
# Locate the project test runner configuration and execute the suite targeting modular entry point exports.
# Query the workspace static analysis configuration and run the module import linter to verify that lightweight entry facades import exclusively from the canonical external core module.
```

**Accept when:**
- All lightweight entry facades successfully compile and resolve exports against the canonical external core module without unresolved references.
- Automated test suites confirm behavioral equivalence across all modular export pathways.
- Static analysis checks pass with zero reported violations of module boundary delegation rules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>