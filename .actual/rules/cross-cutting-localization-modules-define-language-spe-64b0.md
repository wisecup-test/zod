---
version: 2
name: cross-cutting-localization-modules-define-language-spe-64b0
description: "Internal Core Module Integration for Localization Modules: Localization Modules Define Language Specific Grammatical"
metadata:
  actual:
    adr_id: 64b00cb1-2ea2-48e9-b67f-615108520386
    status: accepted
    candidate_group_id: a9c62ae4-f0d0-459b-84d7-cef8e7278899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/locales/**
---

# Internal Core Module Integration for Localization Modules: Localization Modules Define Language Specific Grammatical

Scope: applies to `packages/zod/src/v4/locales/**`.

These rules are ALWAYS ACTIVE for:
- All internal localization modules responsible for translating or formatting validation error messages.
- Internal core modules providing shared checks, error specifications, and utilities.

### Rules

- **R-LM-001** MAY: Localization modules MAY define language-specific grammatical rules and string interpolation logic while delegating validation and error structures to the core module.

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
