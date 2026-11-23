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

These rules are ALWAYS ACTIVE for:
- Internal core library modules responsible for schema definition, compilation routines, and validation checks.
- Runtime compilation and method installation mechanisms wrapping parser functions.

### Rules

- **R-LM-001** MUST: All core validation, parsing, and compilation capabilities MUST be structured as dedicated internal library modules that encapsulate checks, schemas, and compilation routines behind explicit modular boundaries.

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
