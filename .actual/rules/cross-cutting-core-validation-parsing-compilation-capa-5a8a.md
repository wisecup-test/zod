---
version: 2
name: cross-cutting-core-validation-parsing-compilation-capa-5a8a
description: "Core Library Module Architecture: Core Validation Parsing Compilation Capabilities Structured"
metadata:
  actual:
    adr_id: 5a8a1a19-5770-493a-b3eb-f887e1a336ee
    status: accepted
    candidate_group_id: a51e0918-ebb5-4091-bf89-5c5aaedb2d07
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Library Module Architecture: Core Validation Parsing Compilation Capabilities Structured

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for internal core library modules responsible for schema definition, compilation routines, validation checks, and runtime compilation/method installation mechanisms.

### Rules

- **R-CORE-001** MUST: All core validation, parsing, and compilation capabilities MUST be structured as dedicated internal library modules that encapsulate checks, schemas, and compilation routines behind explicit modular boundaries.
- **R-CORE-002** MUST: When installing compiled methods via `installCompiledUserMethods`, wrap target `parse` and `safeParse` functions with fallback delegation to original source implementations.
- **R-CORE-003** MUST: Scope contextual compiler caches and state mappings to active evaluation cycles to prevent unbounded memory growth, and explicitly clear contextual constants and registries upon completion of schema processing runs.
- **R-CORE-004** MUST: Enforce strict module hierarchy rules and automated linting to prevent cyclic cross-module imports between core modules.

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