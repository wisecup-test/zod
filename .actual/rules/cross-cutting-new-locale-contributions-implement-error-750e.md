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

These rules are ALWAYS ACTIVE for all localization definitions, internationalization message formatting modules, and extensions or contributions providing new language message maps.

### Rules

- **R-ZOD-001** SHOULD: New locale contributions SHOULD implement error mapping functions by mapping internal core issue codes to localized message templates.
- **R-ZOD-002** MANDATORY: Discover the internal core module export surface to identify available check types, error models, and string utility routines before authoring new locale definitions.
- **R-ZOD-003** MANDATORY: Ensure all localized message factories conform to the error formatting signature expected by the core error handling subsystem.
- **R-ZOD-004** MANDATORY: Execute lock-version grounding (find dependency manifest, identify build tool, inspect lock/resolution artifact, lookup official documentation for exact version, confirm API existence, and re-run per dependency at point of use) before writing code that uses a versioned library.

### Verify

```bash
# Discover the project task runner configuration and execute the static type-checking and linting suites to ensure locale imports satisfy internal core module boundaries.
# Discover the test suite execution script from the repository manifest and run all localization unit tests to verify error formatting consistency against core expectations.
```

**Accept when:**
- All localization modules resolve imports directly against the internal core module boundary without missing exports or type errors.
- Automated localization test suites execute and pass across all registered locale targets.
- No duplicate validation check definitions or uncoordinated error structures exist across localization files.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, type checks, and unit test suites must be executed to verify import boundaries and message formatting validations across all locale modules.
</enforcement>