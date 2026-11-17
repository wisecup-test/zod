---
version: 2
name: cross-cutting-lightweight-modular-entry-points-zod-8e30
description: "Zod Shared External Core Module Delegation: Lightweight Modular Entry Points Zod Delegate"
metadata:
  actual:
    adr_id: 8e309c48-4737-4675-9dfb-02aaa569c3b3
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

# Zod Shared External Core Module Delegation: Lightweight Modular Entry Points Zod Delegate

Scope: applies to `packages/zod/src/mini/**`, `packages/zod/src/v4-mini/**`.

These rules are ALWAYS ACTIVE for modular and lightweight package entry point exports within the library workspace and internal submodules providing public or semi-public validation surface definitions.

### Rules

- **R-ZOD-001** MUST: Lightweight modular entry points for Zod MUST delegate core schema capabilities directly to the centralized shared external core module rather than implementing independent runtime logic.
- **R-ZOD-002** MUST: Ensure all re-exported symbols from the shared external core module preserve type definitions and parameter constraints identical to the primary library exports.
- **R-ZOD-003** MUST: Structure entry facades as pure re-export boundaries with minimal to zero runtime initialization code.

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
Claude Code MUST NOT skip or defer verification. All pull requests introducing duplicate core implementations or bypassing the external core module are blocked from merging.
</enforcement>