---
version: 2
name: cross-cutting-consumers-discover-project-dependency-ma-5ee9
description: "Internal Core Module Integration for Localization Modules: Consumers Discover Project Dependency Manifest Authoritative"
metadata:
  actual:
    adr_id: 5ee962d4-ed29-4a11-9ac0-70c58df6d229
    status: accepted
    candidate_group_id: a9c62ae4-f0d0-459b-84d7-cef8e7278899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/locales/**
---

# Internal Core Module Integration for Localization Modules: Consumers Discover Project Dependency Manifest Authoritative

Scope: applies to `packages/zod/src/v4/locales/**`.

These rules are ALWAYS ACTIVE for:
- All internal localization modules responsible for translating or formatting validation error messages.
- Internal core modules providing shared checks, error specifications, and utilities.

### Rules

- **R-LM-001** MUST: Consumers MUST discover the project dependency manifest and authoritative lock artifact to verify exact dependency resolutions prior to modifying or implementing module integrations.

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
