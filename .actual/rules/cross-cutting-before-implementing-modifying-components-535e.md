---
version: 2
name: cross-cutting-before-implementing-modifying-components-535e
description: "React Server Component Client Boundary Demarcation via use client Directive: Before Implementing Modifying Components That Use"
metadata:
  actual:
    adr_id: 535e0981-4a1e-40ae-8d8f-5489aae91f7b
    status: accepted
    candidate_group_id: acff8b33-9c51-4920-90b0-98df262c0044
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Server Component Client Boundary Demarcation via use client Directive: Before Implementing Modifying Components That Use

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all frontend UI components within the documentation and web interface packages requiring interactive state, DOM manipulation, or browser APIs, and integration wrapper components interfacing with client-only third-party UI widgets and search dialogs.

### Rules

- **R-RSC-001** MUST: Before implementing or modifying components that use rendering model directives, the consumer MUST inspect the repository dependency manifest and lock artifact to resolve the exact locked version of the UI framework and related dependencies.
- **R-RSC-002** MUST: Place the directive at the very top of the module file before any import declarations or executable logic.
- **R-RSC-003** MUST: Push client boundaries as far down the component hierarchy as feasible, isolating interactive controls from static documentation content.
- **R-RSC-004** MUST: Pass server-rendered content as children or component props into client boundary components to preserve server rendering benefits for static descendant nodes.

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
Claude Code MUST NOT skip or defer verification. Verification by static analysis, linting, build checks, and peer code review is mandatory.
</enforcement>