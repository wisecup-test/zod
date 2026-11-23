---
version: 2
name: cross-cutting-element-registration-removal-synchronize-a4d1
description: "React Mutable Ref Map Pattern for DOM Node Caching: Element Registration Removal Synchronized Mounting Unmounting"
metadata:
  actual:
    adr_id: a4d14fba-9945-404c-b9c5-d07d4bfc22d5
    status: accepted
    candidate_group_id: 3b215305-688a-477b-83d0-704f562c9c03
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Mutable Ref Map Pattern for DOM Node Caching: Element Registration Removal Synchronized Mounting Unmounting

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for:
- Client-rendered navigation components that measure and track DOM element positions dynamically.
- Components maintaining active indicators synchronized with scroll or focus events.

### Rules

- **R-DAP-001** MUST: Element registration and removal MUST be synchronized with element mounting and unmounting lifecycles using ref callbacks or cleanup functions within lifecycle hooks.

### Verify

- Discover and execute the project test runner to validate component rendering and active element indicator calculations.
- Discover and execute the static type checker to ensure proper typing of ref collections and element map accessors.
- Discover and execute the project linter to enforce hook dependency rules and prevent improper ref modifications during render.

**Accept when:**

- Component tests pass with all target DOM nodes correctly registered, accessed, and cleaned up upon unmount.
- Type checking completes with zero errors across mutable ref definitions and Map operations.
- Lint analysis reports no violations for hook dependency arrays or mutable ref assignments during render.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated pull request continuous integration checks verifying test suites, linting rules, and type compliance.
- Verified by: Peer code review validating correct cleanup logic and preventing reactive state misuse for DOM caching.
- Violation handling: Pull requests introducing state-based DOM element tracking or missing cache cleanup handlers must be rejected.
- Violation handling: Violations identified during code review require refactoring to use the mutable ref Map pattern before merge.
- Exception process: Submit an architectural review request demonstrating that reactive state synchronization is strictly required for the component layout.
- Exception process: Obtain written approval from the frontend architecture lead prior to merging alternative DOM tracking implementations.
</enforcement>
