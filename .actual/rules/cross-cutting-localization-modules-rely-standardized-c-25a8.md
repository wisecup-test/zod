---
version: 2
name: cross-cutting-localization-modules-rely-standardized-c-25a8
description: "Internal Core Module Integration for Localization Modules: Localization Modules Rely Standardized Check Error"
metadata:
  actual:
    adr_id: 25a80af3-0f57-49b4-8cde-c2d08f40ddca
    status: accepted
    candidate_group_id: a9c62ae4-f0d0-459b-84d7-cef8e7278899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/locales/**
---

# Internal Core Module Integration for Localization Modules: Localization Modules Rely Standardized Check Error

Scope: applies to `packages/zod/src/v4/locales/**`.

These rules are ALWAYS ACTIVE for all internal localization modules responsible for translating or formatting validation error messages, and internal core modules providing shared checks, error specifications, and utilities.

### Rules

- **R-LOC-001** SHOULD: Localization modules SHOULD rely on the standardized check, error, and utility contracts exposed by the internal core module to maintain structural parity across all locales.
- **R-LOC-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-LOC-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find the dependency manifest, identify the build tool, inspect the repository lock or resolution artifact, look up official documentation for that exact version, confirm every API/class/function exists in that version's documentation, and re-run steps 3-5 per dependency at point of use.
- **R-LOC-004** MANDATORY: Verify module import paths adhere to internal architectural boundaries when authoring new locale definitions.
- **R-LOC-005** MANDATORY: Ensure error formatting templates consume parameters strictly from core error schemas to preserve contract fidelity.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify module import constraints across localization modules.
# Discover and execute the repository test suite to validate locale error formatting against core check specifications.
```

**Accept when:**
- All localization modules successfully import core checks, errors, and utilities without boundary violations.
- Test suites pass for all locale modules with consistent error formatting behavior.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks verifying module imports and boundary compliance, and peer code review.
</enforcement>