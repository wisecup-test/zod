---
version: 2
name: cross-cutting-runtime-method-compilation-utilize-insta-699c
description: "Core Library Module Architecture: Runtime Method Compilation Utilize Installcompiledusermethods Wrap"
metadata:
  actual:
    adr_id: 699c8ae8-b0c4-469a-ba64-ca162eacbd49
    status: accepted
    candidate_group_id: a51e0918-ebb5-4091-bf89-5c5aaedb2d07
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Library Module Architecture: Runtime Method Compilation Utilize Installcompiledusermethods Wrap

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for internal core library modules responsible for schema definition, compilation routines, and validation checks.

### Rules

- **R-CORE-001** MUST: Runtime method compilation MUST utilize installCompiledUserMethods to wrap core parse and safeParse entrypoints with compiled parser functions while preserving original fallback behavior.
- **R-CORE-002** MUST: Scope contextual compiler caches and state mappings to active evaluation cycles to prevent unbounded memory growth.
- **R-CORE-003** MANDATORY: Execute lock-version grounding before writing code that uses a versioned library (find manifest, identify build tool, inspect lock/resolution artifact, lookup official documentation for exact version, confirm API existence, re-run per dependency at point of use).

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