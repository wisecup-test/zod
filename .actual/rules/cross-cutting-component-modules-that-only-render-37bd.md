---
version: 2
name: cross-cutting-component-modules-that-only-render-37bd
description: "React Server Component Client Boundary Demarcation via use client Directive: Component Modules That Only Render Static"
metadata:
  actual:
    adr_id: 37bd308d-6f92-4a5b-960d-94bad336a0c6
    status: accepted
    candidate_group_id: acff8b33-9c51-4920-90b0-98df262c0044
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Server Component Client Boundary Demarcation via use client Directive: Component Modules That Only Render Static

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all frontend UI components, integration wrappers, and related modules within the project repository.

### Rules

- **R-RSC-001** MUST_NOT: Component modules that only render static props and require no browser APIs, event listeners, or client-side hooks MUST NOT declare the use client directive.

### Verify

```bash
# Discover the project dependency manifest and lock artifact, and verify the exact resolved versions of the UI framework and component libraries.
# Discover and run the project static analysis and linting scripts to verify that client hooks are accompanied by client boundary declarations.
# Discover and execute the project build verification command to confirm clean compilation across server and client component boundaries.
```

**Accept when:**
- All UI components utilizing React state, effects, browser DOM references, or client-only hooks declare the use client directive at the module root.
- Static and server-renderable UI components without interactivity remain free of the use client directive to avoid unnecessary client bundle growth.
- Automated build and static analysis checks pass with zero client boundary syntax or runtime lifecycle errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Compliance is strictly enforced via automated static analysis, linting, build pipelines, and mandatory peer code review.
</enforcement>