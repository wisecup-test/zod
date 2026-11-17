---
version: 2
name: cross-cutting-intermediate-compiler-representations-sc-f7ae
description: "Core Library Module Architecture: Intermediate Compiler Representations Schema Transformations Coordinated"
metadata:
  actual:
    adr_id: f7aecc82-59ba-4462-bfda-130385d31300
    status: accepted
    candidate_group_id: a51e0918-ebb5-4091-bf89-5c5aaedb2d07
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Library Module Architecture: Intermediate Compiler Representations Schema Transformations Coordinated

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for internal core library modules responsible for schema definition, compilation routines, and validation checks.

### Rules

- **R-COR-001** SHOULD: Intermediate compiler representations and schema transformations SHOULD be coordinated through contextual cache lookups and dedicated registries rather than redundant re-computation.
- **R-COR-002** MANDATORY: When installing compiled methods via installCompiledUserMethods, wrap target parse and safeParse functions with fallback delegation to original source implementations.
- **R-COR-003** MANDATORY: Scope contextual compiler caches and state mappings to active evaluation cycles to prevent unbounded memory growth.
- **R-COR-004** MANDATORY: Enforce strict module hierarchy rules and automated linting to prevent cyclic cross-module imports.
- **R-COR-005** MANDATORY: Explicitly clear contextual constants and registries upon completion of schema processing runs.
- **R-COR-006** MANDATORY: Consumer MUST discover build tools, dependencies, and exact versions from the repository manifest, lockfile, and official documentation (Lock-Version Grounding).

### Verify

```bash
# Discover and execute the repository build verification script to validate module resolution across all core library boundaries.
# Discover and run the project test suite targeting core schema compilation, parsing, and validation check routines.
# Discover and run the repository static type checker and module linting tools to confirm interface compliance and absence of circular references.
```

**Accept when:**
- All unit tests covering core schema compilation, parsing, and check validations pass cleanly.
- Static type analysis confirms that function signatures and compiled method wrappers adhere to declared interfaces with zero type errors.
- Module boundary analysis verifies no undeclared cyclic references exist between core library modules.

<enforcement>
Verification is mandatory. Claude Code MUST NOT skip or defer verification.
</enforcement>