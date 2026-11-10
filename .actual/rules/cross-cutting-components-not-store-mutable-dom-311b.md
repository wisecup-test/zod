---
version: 2
name: cross-cutting-components-not-store-mutable-dom-311b
description: "React Mutable Ref Map Pattern for DOM Node Caching: Components Not Store Mutable Dom Element"
metadata:
  actual:
    adr_id: 311b950c-1e80-4452-bd6d-33bece33dc9a
    status: accepted
    candidate_group_id: 3b215305-688a-477b-83d0-704f562c9c03
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Mutable Ref Map Pattern for DOM Node Caching: Components Not Store Mutable Dom Element

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for client-rendered navigation components that measure and track DOM element positions dynamically and components maintaining active indicators synchronized with scroll or focus events.

### Rules

- **R-REACT-001** MUST_NOT: Components MUST_NOT store mutable DOM element references in reactive component state when the updates do not alter the rendered markup hierarchy.

### Verify

```bash
# Discover and execute project test runner
# Discover and execute static type checker
# Discover and execute project linter
```

**Accept when:**
- Component tests pass with all target DOM nodes correctly registered, accessed, and cleaned up upon unmount.
- Type checking completes with zero errors across mutable ref definitions and Map operations.
- Lint analysis reports no violations for hook dependency arrays or mutable ref assignments during render.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated CI checks, peer code review, and manual architectural review enforce these rules.
</enforcement>