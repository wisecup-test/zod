---
version: 2
name: cross-cutting-compilation-routines-register-contextual-5b19
description: "Core Library Module Architecture: Compilation Routines Register Contextual Constants Schema"
metadata:
  actual:
    adr_id: 5b191393-16af-44e3-8528-813513e43552
    status: accepted
    candidate_group_id: a51e0918-ebb5-4091-bf89-5c5aaedb2d07
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Library Module Architecture: Compilation Routines Register Contextual Constants Schema

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for internal core library modules responsible for schema definition, compilation routines, validation checks, and runtime compilation/method installation mechanisms.

### Rules

- **R-CORE-001** MAY: Compilation routines MAY register contextual constants and schema mappings into execution context tables to accelerate recursive evaluation.

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
Claude Code MUST NOT skip or defer verification.
</enforcement>