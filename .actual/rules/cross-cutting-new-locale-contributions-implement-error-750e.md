---
version: 2
name: cross-cutting-new-locale-contributions-implement-error-750e
description: "Zod Core Internal Module Architecture: New Locale Contributions Implement Error Mapping"
metadata:
  actual:
    adr_id: 750e7eb1-4992-4c14-9702-db8f4b72affd
    status: accepted
    candidate_group_id: a22d8aec-faab-4dfb-9104-b031f65251b9
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Zod Core Internal Module Architecture: New Locale Contributions Implement Error Mapping

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for:
- All localization definitions and internationalization message formatting modules within the library.
- Extensions and contributions providing new language message maps.

### Rules

- **R-LM-001** SHOULD: New locale contributions SHOULD implement error mapping functions by mapping internal core issue codes to localized message templates.

### Verify

- Discover the project task runner configuration and execute the static type-checking and linting suites to ensure locale imports satisfy internal core module boundaries.
- Discover the test suite execution script from the repository manifest and run all localization unit tests to verify error formatting consistency against core expectations.

**Accept when:**

- All localization modules resolve imports directly against the internal core module boundary without missing exports or type errors.
- Automated localization test suites execute and pass across all registered locale targets.
- No duplicate validation check definitions or uncoordinated error structures exist across localization files.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis and type checks verifying import boundaries on every pull request.
- Verified by: Unit test suites executing message formatting validations across all locale modules.
- Verified by: Peer review by library maintainers for any newly proposed localization modules.
- Violation handling: Pull requests introducing foreign imports or duplicated check logic into localization modules will fail automated checks and require remediation before merge.
- Violation handling: Discovered regressions or non-conforming locale definitions will be tracked as blocking issues.
- Exception process: Exceptions requiring custom formatting logic must be submitted as architectural change requests to core maintainers, seeking extension of internal core utilities rather than localized workarounds.
</enforcement>
