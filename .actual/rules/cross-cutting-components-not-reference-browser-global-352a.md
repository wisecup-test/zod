---
version: 2
name: cross-cutting-components-not-reference-browser-global-352a
description: "React Client Component Interaction Architecture: Components Not Reference Browser Global Objects"
metadata:
  actual:
    adr_id: 352a4d32-ca4c-4ac2-8b36-c58333a8a8b5
    status: accepted
    candidate_group_id: f9a2d8cc-8daa-42ab-90ec-25b61d21e072
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Client Component Interaction Architecture: Components Not Reference Browser Global Objects

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for:
- All interactive UI components authoring client-side state, DOM manipulation, or third-party client integrations in frontend documentation packages.

### Rules

- **R-IP-001** MUST_NOT: Components MUST NOT reference browser global objects or perform DOM mutations outside of client lifecycle hooks or client event handlers.

### Verify

- Discover the workspace static analysis script from the project manifest and run it to verify compliance with hook usage and client directive requirements.
- Discover the project automated test script from the project manifest and execute it to validate interactive component behavior and state transitions.
- Discover the project type checking script from the project manifest and run it to verify type safety across component props and hook dependencies.

**Accept when:**

- All interactive UI components declare the client directive at the module root and pass static analysis without lint violations.
- All component interaction tests execute successfully with zero unhandled exceptions or effect lifecycle warnings.
- Static type checking completes with zero diagnostic errors across all client component files.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline executing static analysis and lint checks.
- Verified by: Peer code review verifying component boundary placement and effect cleanup logic.
- Violation handling: Pull requests containing unencapsulated browser API access or missing client directives are blocked by continuous integration checks.
- Violation handling: Identified violations must be refactored into compliant client component hooks before merging.
- Exception process: Submit an architectural variance request documented in the relevant pull request outlining why a non-standard interaction mechanism is required.
- Exception process: Obtain approval from the frontend architecture lead prior to merging.
</enforcement>
