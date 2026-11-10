---
version: 2
name: cross-cutting-localization-definitions-not-define-inde-f0db
description: "Zod Core Internal Module Architecture: Localization Definitions Not Define Independent Error"
metadata:
  actual:
    adr_id: f0dbf828-25f3-4433-93fe-a9de312054e1
    status: accepted
    candidate_group_id: a22d8aec-faab-4dfb-9104-b031f65251b9
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Zod Core Internal Module Architecture: Localization Definitions Not Define Independent Error

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST_NOT: Localization definitions MUST_NOT define independent error structures or duplicate core validation check logic outside of the established internal core library interfaces.

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