---
version: 2
name: cross-cutting-shared-components-that-accept-code-8c83
description: "Adoption of Shared Internal Module `@/components/inline-code-title` for Code Title Presentation: Shared Components That Accept Code Titles"
metadata:
  actual:
    adr_id: 8c837bdb-dc73-44ac-a6e5-f176e426653f
    status: accepted
    candidate_group_id: bedfd70d-2d50-4010-8699-3f33e118e97e
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/blog/**
      - components/**
---

# Adoption of Shared Internal Module `@/components/inline-code-title` for Code Title Presentation: Shared Components That Accept Code Titles

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CODE-TITLE-001** SHOULD: Shared UI components that accept code titles SHOULD accept standard title property types defined by `@/components/inline-code-title` to preserve semantic markup.

### Verify

```bash
# Discover and execute repository static analysis / linting to check import statements
# Discover and run project type checking and test suites
```

**Accept when:**
- All documentation pages, blog views, navigation components, and syndication endpoints import code title rendering from the centralized internal module without unresolved path errors.
- Project static analysis, type verification, and test suites pass without violations regarding unshared inline code title implementations.

<enforcement>
Verification is mandatory. Claude Code MUST NOT skip or defer verification.
</enforcement>