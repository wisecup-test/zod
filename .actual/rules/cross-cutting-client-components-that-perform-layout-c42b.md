---
version: 2
name: cross-cutting-client-components-that-perform-layout-c42b
description: "React Mutable Ref Map Pattern for DOM Node Caching: Client Components That Perform Layout Measurement"
metadata:
  actual:
    adr_id: c42b0e3b-0876-4e10-8d6a-6435c5d563c7
    status: accepted
    candidate_group_id: 3b215305-688a-477b-83d0-704f562c9c03
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Mutable Ref Map Pattern for DOM Node Caching: Client Components That Perform Layout Measurement

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-REF-001** MUST: Client components that perform layout measurement or active scroll tracking on dynamic element collections MUST adopt a React mutable reference encapsulating an in-memory Map to cache DOM node references.

### Verify

```bash
# Discover and execute the project test runner to validate component rendering and active element indicator calculations.
# Discover and execute the static type checker to ensure proper typing of ref collections and element map accessors.
# Discover and execute the project linter to enforce hook dependency rules and prevent improper ref modifications during render.
```

**Accept when:**
- Component tests pass with all target DOM nodes correctly registered, accessed, and cleaned up upon unmount.
- Type checking completes with zero errors across mutable ref definitions and Map operations.
- Lint analysis reports no violations for hook dependency arrays or mutable ref assignments during render.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated pull request checks, peer code review, and strict adherence to the mutable ref Map pattern.
</enforcement>