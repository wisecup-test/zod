---
version: 2
name: cross-cutting-internal-core-modules-expose-minimal-0acf
description: "Internal Core Module Integration for Localization Modules: Internal Core Modules Expose Minimal Stable"
metadata:
  actual:
    adr_id: 0acf7835-09d6-4510-8b54-a36306cf70b0
    status: accepted
    candidate_group_id: a9c62ae4-f0d0-459b-84d7-cef8e7278899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/locales/**
---

# Internal Core Module Integration for Localization Modules: Internal Core Modules Expose Minimal Stable

Scope: applies to `packages/zod/src/v4/locales/**`.

These rules are ALWAYS ACTIVE for:
- All internal localization modules responsible for translating or formatting validation error messages.
- Internal core modules providing shared checks, error specifications, and utilities.

### Rules

- **R-LM-001** MUST: Internal core modules MUST expose minimal, stable interfaces for checks, errors, and utilities while encapsulating common evaluation mechanisms.

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
