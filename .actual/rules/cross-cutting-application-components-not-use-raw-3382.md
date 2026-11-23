---
version: 2
name: cross-cutting-application-components-not-use-raw-3382
description: "next/link Client Navigation Module Adoption: Application Components Not Use Raw Html"
metadata:
  actual:
    adr_id: 33828e4b-2e42-4c83-b2d7-c81c26bc2b64
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

# next/link Client Navigation Module Adoption: Application Components Not Use Raw Html

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for:
- All page views and interactive UI components requiring navigation between internal application routes.

### Rules

- **R-LM-001** MUST_NOT: Application components MUST NOT use raw HTML anchor elements for internal route navigation when declarative client routing is available.

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
