---
version: 2
name: cross-cutting-core-modules-not-introduce-circular-2434
description: "Core Library Module Architecture: Core Modules Not Introduce Circular Imports"
metadata:
  actual:
    adr_id: 243443a2-f390-4b35-8da7-75e24464205a
    status: accepted
    candidate_group_id: a51e0918-ebb5-4091-bf89-5c5aaedb2d07
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Library Module Architecture: Core Modules Not Introduce Circular Imports

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for:
- Internal core library modules responsible for schema definition, compilation routines, and validation checks.
- Runtime compilation and method installation mechanisms wrapping parser functions.

### Rules

- **R-LM-001** MUST_NOT: Core modules MUST NOT introduce circular imports across internal subsystem domains or mutate public parser contracts without designated installation wrappers.

### Verify

- Discover and execute the repository build verification script to validate module resolution across all core library boundaries.
- Discover and run the project test suite targeting core schema compilation, parsing, and validation check routines.
- Discover and run the repository static type checker and module linting tools to confirm interface compliance and absence of circular references.

**Accept when:**

- All unit tests covering core schema compilation, parsing, and check validations pass cleanly.
- Static type analysis confirms that function signatures and compiled method wrappers adhere to declared interfaces with zero type errors.
- Module boundary analysis verifies no undeclared cyclic references exist between core library modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Continuous integration suites verifying module boundaries and running core unit tests.
- Verified by: Static type checking ensuring structural compliance with compiled function and schema interfaces.
- Verified by: Code reviews by core library maintainers for any changes to internal module structure.
- Violation handling: Automated build failures on circular dependencies or unauthorized module boundary violations.
- Violation handling: Rejection of pull requests that mutate public parser contracts without using approved installation wrappers.
- Exception process: Engineers must submit an architectural exception request detailing technical blockers to core module decoupling.
- Exception process: Exceptions require unanimous approval from core library maintainers and must include an issue tracker reference for future remediation.
</enforcement>
