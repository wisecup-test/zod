---
version: 2
name: cross-cutting-input-parsing-invoke-parse-method-3ada
description: "Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Input Parsing Invoke Parse Method Defined"
metadata:
  actual:
    adr_id: 3ada0d44-da04-47f4-8577-df7f217de30e
    status: accepted
    candidate_group_id: 4ecfb3a9-b029-42f8-9301-7d71eb684470
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Input Parsing Invoke Parse Method Defined

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: Input parsing MUST invoke the parse method on defined schemas to enforce structural and constraint compliance at runtime boundaries.

### Verify

```bash
# Discover dependency manifest and lock file for schema validation library
# Run the project automated test suite via repository script runner
npm test

# Run project static type checker and linter
npm run lint
npm run typecheck
```

**Accept when:**
- All schema validation invocations resolve through the modular functional entrypoint without importing monolithic packages.
- Input parsing tests successfully verify structural and constraint assertions using schema parse methods.
- Static analysis and type checking pass without errors across all modules declaring validation schemas.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>