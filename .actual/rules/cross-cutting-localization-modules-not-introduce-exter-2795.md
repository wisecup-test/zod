---
version: 2
name: cross-cutting-localization-modules-not-introduce-exter-2795
description: "Zod Core Internal Module Architecture: Localization Modules Not Introduce External Runtime"
metadata:
  actual:
    adr_id: 27957c44-4e6d-4352-bebd-918ed0441de8
    status: accepted
    candidate_group_id: a22d8aec-faab-4dfb-9104-b031f65251b9
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Zod Core Internal Module Architecture: Localization Modules Not Introduce External Runtime

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all localization definitions and internationalization message formatting modules within the library.

### Rules

- **R-LOC-001** SHOULD_NOT: Localization modules SHOULD_NOT introduce external runtime dependencies beyond the internal core library modules.

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
Claude Code MUST NOT skip or defer verification.
</enforcement>