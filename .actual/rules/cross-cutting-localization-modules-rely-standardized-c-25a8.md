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

These rules are ALWAYS ACTIVE for:
- All internal localization modules responsible for translating or formatting validation error messages.
- Internal core modules providing shared checks, error specifications, and utilities.

### Rules

- **R-LM-001** SHOULD: Localization modules SHOULD rely on the standardized check, error, and utility contracts exposed by the internal core module to maintain structural parity across all locales.

### Verify

- Discover and run the project static analysis and linting scripts to verify module import constraints across localization modules.
- Discover and execute the repository test suite to validate locale error formatting against core check specifications.

**Accept when:**

- All localization modules successfully import core checks, errors, and utilities without boundary violations.
- Test suites pass for all locale modules with consistent error formatting behavior.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks verifying module imports and boundary compliance.
- Verified by: Peer code review for all new and modified localization modules.
- Violation handling: Pull requests with non-compliant imports or duplicated core logic are blocked from merging.
- Violation handling: Violations must be refactored to consume the shared core module before approval.
- Exception process: Exceptions require formal architectural review and approval documented in a follow-up decision record.
</enforcement>
