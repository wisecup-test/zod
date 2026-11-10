---
version: 2
name: cross-cutting-client-boundary-components-accept-server-dde9
description: "React Server Component Client Boundary Demarcation via use client Directive: Client Boundary Components Accept Server Rendered"
metadata:
  actual:
    adr_id: dde914bc-baa4-4cce-b5e5-fc9bcf5c6993
    status: accepted
    candidate_group_id: acff8b33-9c51-4920-90b0-98df262c0044
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Server Component Client Boundary Demarcation via use client Directive: Client Boundary Components Accept Server Rendered

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all frontend UI components within the documentation and web interface packages requiring interactive state, DOM manipulation, or browser APIs, and integration wrapper components interfacing with client-only third-party UI widgets and search dialogs.

### Rules

- **R-CLI-001** MAY: Client boundary components MAY accept server-rendered React nodes as children or props to compose server and client rendering without converting child trees into client components.

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
Claude Code MUST NOT skip or defer verification. Compliance is verified by static analysis rules, linting checks, and automated build verification in the CI pipeline.
</enforcement>