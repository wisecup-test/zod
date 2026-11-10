---
version: 2
name: cross-cutting-engineers-discover-repository-dependency-3789
description: "Zod Shared External Core Module Delegation: Engineers Discover Repository Dependency Resolution Artifact"
metadata:
  actual:
    adr_id: 37891c8c-4595-4f47-a1e1-0d9796ed1cb5
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

# Zod Shared External Core Module Delegation: Engineers Discover Repository Dependency Resolution Artifact

Scope: applies to `packages/zod/src/mini/**`, `packages/zod/src/v4-mini/**`.

These rules are ALWAYS ACTIVE for modular and lightweight package entry point exports within the library workspace and internal submodules providing public or semi-public validation surface definitions.

### Rules

- **R-ZOD-001** MUST: Engineers MUST discover the repository dependency resolution artifact to determine the exact resolved version of all internal workspace and library dependencies prior to referencing shared core exports.

### Verify

```bash
# Discover repository build script and compile to validate module export compatibility
# Locate test runner configuration and execute suite targeting modular entry point exports
# Run module import linter to verify lightweight entry facades import exclusively from the canonical external core module
```

**Accept when:**
- All lightweight entry facades successfully compile and resolve exports against the canonical external core module without unresolved references.
- Automated test suites confirm behavioral equivalence across all modular export pathways.
- Static analysis checks pass with zero reported violations of module boundary delegation rules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines, peer code review, and static analysis linting rules enforce module export integrity, type signatures, and delegation to the canonical external core module.
</enforcement>