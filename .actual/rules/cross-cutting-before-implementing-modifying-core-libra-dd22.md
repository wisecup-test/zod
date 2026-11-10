---
version: 2
name: cross-cutting-before-implementing-modifying-core-libra-dd22
description: "Core Library Module Architecture: Before Implementing Modifying Core Library Interfaces"
metadata:
  actual:
    adr_id: dd223844-7690-4295-b10e-b4766ce9ef4d
    status: accepted
    candidate_group_id: a51e0918-ebb5-4091-bf89-5c5aaedb2d07
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Library Module Architecture: Before Implementing Modifying Core Library Interfaces

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for internal core library modules, schema definition, compilation routines, validation checks, and runtime compilation/method installation mechanisms.

### Rules

- **R-CORE-001** MUST: Before implementing or modifying core library interfaces, consumers MUST discover the project dependency manifest and authoritative resolution artifact to verify exact locked versions.
- **R-CORE-002** MUST: Wrap target parse and safeParse functions with fallback delegation to original source implementations when installing compiled methods via installCompiledUserMethods.
- **R-CORE-003** MUST: Scope contextual compiler caches and state mappings to active evaluation cycles to prevent unbounded memory growth.

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
Claude Code MUST NOT skip or defer verification. Continuous integration suites, static type checking, and code reviews enforce module boundaries and core unit tests.
</enforcement>