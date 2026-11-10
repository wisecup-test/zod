---
version: 2
name: cross-cutting-localization-modules-expose-custom-helpe-c7c2
description: "Zod Core Internal Module Architecture: Localization Modules Expose Custom Helper Functions"
metadata:
  actual:
    adr_id: c7c2e950-c796-461a-8549-2362ad0def9a
    status: accepted
    candidate_group_id: a22d8aec-faab-4dfb-9104-b031f65251b9
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Zod Core Internal Module Architecture: Localization Modules Expose Custom Helper Functions

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all localization definitions and internationalization message formatting modules within the library, and extensions and contributions providing new language message maps.

### Rules

- **R-ZOD-LOC-001** MAY: Localization modules MAY expose custom helper functions for language-specific grammatical inflection provided they consume base message structures from the internal core library utilities.

### Verify

```bash
# Discover the project task runner configuration and execute the static type-checking and linting suites
# Example: npm run lint / npx tsc --noEmit (derive actual commands from repository manifest)

# Discover and run the test suite execution script from the repository manifest for localization tests
# Example: npm test
```

**Accept when:**
- All localization modules resolve imports directly against the internal core module boundary without missing exports or type errors.
- Automated localization test suites execute and pass across all registered locale targets.
- No duplicate validation check definitions or uncoordinated error structures exist across localization files.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, type checks, and unit test suites must be executed as defined in the repository manifest.
</enforcement>