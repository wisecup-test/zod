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

These rules are ALWAYS ACTIVE for:
- All page views and interactive UI components requiring navigation between internal application routes.

### Rules

- **R-LM-001** SHOULD: Components implementing custom interactive triggers or styled wrappers around next/link SHOULD maintain accessible anchor semantics and keyboard focus behaviors.

### Verify

- Discover and execute the repository static analysis and linting scripts to identify non-compliant anchor usage.
- Discover and execute the repository test runner to verify navigation component rendering and routing integrity.

**Accept when:**

- All internal navigation hyperlinks render through next/link without unmanaged anchor element fallbacks.
- Repository static analysis and test validation suites pass without routing rule violations.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Static analysis and lint checks in continuous integration pipelines.
- Verified by: Code reviews of pull requests introducing or modifying routing components.
- Violation handling: Build failure when disallowed anchor tags are detected for internal routes.
- Violation handling: Review rejection during pull request evaluation.
- Exception process: Submit an architectural exception request documenting requirements for external routing or legacy anchor integration.
- Exception process: Obtain approval from architecture leads prior to merging.
</enforcement>
