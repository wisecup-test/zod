---
version: 2
name: cross-cutting-modules-that-import-client-only-0f85
description: "React Server Component Client Boundary Demarcation via use client Directive: Modules That Import Client Only Navigation"
metadata:
  actual:
    adr_id: 0f852903-b9ab-4b76-b981-133cfce8ca8a
    status: accepted
    candidate_group_id: acff8b33-9c51-4920-90b0-98df262c0044
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Server Component Client Boundary Demarcation via use client Directive: Modules That Import Client Only Navigation

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-RSC-001** MUST: Modules that import client-only navigation hooks, browser storage APIs, or window event listeners MUST declare the use client directive at the module boundary.

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
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines, automated static analysis, build verification, and peer code reviews enforce compliance.
</enforcement>