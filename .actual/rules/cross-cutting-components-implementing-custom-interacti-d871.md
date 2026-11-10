---
version: 2
name: cross-cutting-components-implementing-custom-interacti-d871
description: "next/link Client Navigation Module Adoption: Components Implementing Custom Interactive Triggers Styled"
metadata:
  actual:
    adr_id: d871214c-c2c2-4dcd-b5a4-f8bc516dd7d7
    status: accepted
    candidate_group_id: 8497fb63-f882-4406-98b2-b60281fa558a
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/blog/**
      - components/**
---

# next/link Client Navigation Module Adoption: Components Implementing Custom Interactive Triggers Styled

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-NAV-001** SHOULD: Components implementing custom interactive triggers or styled wrappers around next/link SHOULD maintain accessible anchor semantics and keyboard focus behaviors.
- **R-NAV-002** MANDATORY: Wrap next/link instances in presentation components when applying design system utility styling or responsive layout rules.
- **R-NAV-003** MANDATORY: Ensure passing appropriate accessibility attributes and destination href values to maintain keyboard navigability and semantic structure.

### Verify

```bash
# Discover and execute the repository static analysis and linting scripts to identify non-compliant anchor usage.
# Discover and execute the repository test runner to verify navigation component rendering and routing integrity.
```

**Accept when:**
- All internal navigation hyperlinks render through next/link without unmanaged anchor element fallbacks.
- Repository static analysis and test validation suites pass without routing rule violations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via static analysis, lint checks, and code reviews in continuous integration pipelines.
</enforcement>