---
version: 2
name: cross-cutting-localization-modules-import-consume-shar-064c
description: "Zod Core Internal Module Architecture: Localization Modules Import Consume Shared Validation"
metadata:
  actual:
    adr_id: 064c9fb4-7f39-4214-856d-c2cb9b6faa10
    status: accepted
    candidate_group_id: a22d8aec-faab-4dfb-9104-b031f65251b9
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Zod Core Internal Module Architecture: Localization Modules Import Consume Shared Validation

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-LOC-001** MUST: Localization modules MUST import and consume shared validation checks, error representations, and utility helpers exclusively from the internal core library modules.

### Verify

```bash
# Discover the project task runner configuration and execute the static type-checking and linting suites
# Discover the test suite execution script from the repository manifest and run all localization unit tests
# (Repository-specific commands derived from project manifest and task runner)
```

**Accept when:**
- All localization modules resolve imports directly against the internal core module boundary without missing exports or type errors.
- Automated localization test suites execute and pass across all registered locale targets.
- No duplicate validation check definitions or uncoordinated error structures exist across localization files.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>