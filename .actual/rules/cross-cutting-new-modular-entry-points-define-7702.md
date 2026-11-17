---
version: 2
name: cross-cutting-new-modular-entry-points-define-7702
description: "Zod Shared External Core Module Delegation: New Modular Entry Points Define Specialized"
metadata:
  actual:
    adr_id: 77022841-7403-4e43-9ce1-e8f8ceaf6e53
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

# Zod Shared External Core Module Delegation: New Modular Entry Points Define Specialized

Scope: applies to `packages/zod/src/mini/**`, `packages/zod/src/v4-mini/**`.

These rules are ALWAYS ACTIVE for modular lightweight distribution variants and internal submodules providing public or semi-public validation surface definitions.

### Rules

- **R-MOD-001** MAY: New modular entry points MAY define specialized re-export groupings provided they source primitive definitions strictly from the canonical external core module.
- **R-MOD-002** MANDATORY: Ensure all re-exported symbols from the shared external core module preserve type definitions and parameter constraints identical to the primary library exports.
- **R-MOD-003** MANDATORY: Structure entry facades as pure re-export boundaries with minimal to zero runtime initialization code.
- **R-MOD-004** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: find the dependency manifest, identify the build tool, inspect the repository lock or resolution artifact to determine the exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps per dependency at point of use.

### Verify

```bash
# Discover the repository build script from the project manifest and execute compilation verification:
# (Example: pnpm build / npm run build)
# Locate the project test runner and execute the test suite targeting modular entry points:
# (Example: pnpm test)
# Run the module import linter to verify lightweight entry facades import exclusively from the canonical external core module.
```

**Accept when:**
- All lightweight entry facades successfully compile and resolve exports against the canonical external core module without unresolved references.
- Automated test suites confirm behavioral equivalence across all modular export pathways.
- Static analysis checks pass with zero reported violations of module boundary delegation rules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification by automated CI, peer review, and static analysis linting is mandatory. Violations will block code merging and require refactoring to delegate directly to the canonical external core export.
</enforcement>