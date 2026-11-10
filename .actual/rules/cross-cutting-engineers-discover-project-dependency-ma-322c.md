---
version: 2
name: cross-cutting-engineers-discover-project-dependency-ma-322c
description: "Zod Core Internal Module Architecture: Engineers Discover Project Dependency Manifest Resolve"
metadata:
  actual:
    adr_id: 322c5748-6cb1-413b-97b2-e916afe81e45
    status: accepted
    candidate_group_id: a22d8aec-faab-4dfb-9104-b031f65251b9
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Zod Core Internal Module Architecture: Engineers Discover Project Dependency Manifest Resolve

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all localization definitions, internationalization message formatting modules, and extensions or contributions providing new language message maps within the library.

### Rules

- **R-ZOD-001** MUST: Engineers MUST discover the project dependency manifest and resolve the exact locked version of the validation library from the project lock artifact prior to modifying or implementing localized error maps.

### Verify

```bash
# Discover the project task runner configuration and execute the static type-checking and linting suites
# Discover the test suite execution script from the repository manifest and run all localization unit tests
```

**Accept when:**
- All localization modules resolve imports directly against the internal core module boundary without missing exports or type errors.
- Automated localization test suites execute and pass across all registered locale targets.
- No duplicate validation check definitions or uncoordinated error structures exist across localization files.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis, type checks, and unit test suites executing message formatting validations.
</enforcement>