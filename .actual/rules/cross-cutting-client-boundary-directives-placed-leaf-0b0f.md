---
version: 2
name: cross-cutting-client-boundary-directives-placed-leaf-0b0f
description: "React Server Component Client Boundary Demarcation via use client Directive: Client Boundary Directives Placed Leaf Level"
metadata:
  actual:
    adr_id: 0b0f5a30-c8f7-4d9b-8f3c-c45fd4d57d85
    status: accepted
    candidate_group_id: acff8b33-9c51-4920-90b0-98df262c0044
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Server Component Client Boundary Demarcation via use client Directive: Client Boundary Directives Placed Leaf Level

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all frontend UI components requiring interactive state, DOM manipulation, or browser APIs within the documentation and web interface packages.

### Rules

- **R-CBD-001** SHOULD: Client boundary directives SHOULD be placed at leaf-level interactive components to maximize server-rendered markup and minimize client bundle size.

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
Claude Code MUST NOT skip or defer verification. Compliance with these rules is mandatory and enforced via continuous integration static analysis, linting, and build verification checks.
</enforcement>