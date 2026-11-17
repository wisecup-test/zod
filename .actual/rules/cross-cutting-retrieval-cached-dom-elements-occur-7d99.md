---
version: 2
name: cross-cutting-retrieval-cached-dom-elements-occur-7d99
description: "React Mutable Ref Map Pattern for DOM Node Caching: Retrieval Cached Dom Elements Occur Directly"
metadata:
  actual:
    adr_id: 7d992177-ec2a-4a5b-99fe-8257ca79a966
    status: accepted
    candidate_group_id: 3b215305-688a-477b-83d0-704f562c9c03
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Mutable Ref Map Pattern for DOM Node Caching: Retrieval Cached Dom Elements Occur Directly

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for client-rendered navigation components that measure and track DOM element positions dynamically, and components maintaining active indicators synchronized with scroll or focus events.

### Rules

- **R-DOM-001** SHOULD: Retrieval of cached DOM elements SHOULD occur directly from the mutable ref Map during layout measurement routines rather than through global document queries.

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