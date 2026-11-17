---
version: 2
name: cross-cutting-components-wrap-cache-accessor-modifier-ed1f
description: "React Mutable Ref Map Pattern for DOM Node Caching: Components Wrap Cache Accessor Modifier Functions"
metadata:
  actual:
    adr_id: ed1f4bdd-e886-4a15-97e1-7e9d4e309500
    status: accepted
    candidate_group_id: 3b215305-688a-477b-83d0-704f562c9c03
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Mutable Ref Map Pattern for DOM Node Caching: Components Wrap Cache Accessor Modifier Functions

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for client-rendered navigation components that measure and track DOM element positions dynamically, and components maintaining active indicators synchronized with scroll or focus events.

### Rules

- **R-ADR-001** SHOULD: Components wrap cache accessor and modifier functions in memoized callbacks to prevent recreation across render cycles.

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
Claude Code MUST NOT skip or defer verification.
</enforcement>