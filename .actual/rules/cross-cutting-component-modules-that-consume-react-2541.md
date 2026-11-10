---
version: 2
name: cross-cutting-component-modules-that-consume-react-2541
description: "React Server Component Client Boundary Demarcation via use client Directive: Component Modules That Consume React State"
metadata:
  actual:
    adr_id: 2541a6b7-5e5f-4f79-b0bd-3435d8d1fabd
    status: accepted
    candidate_group_id: acff8b33-9c51-4920-90b0-98df262c0044
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Server Component Client Boundary Demarcation via use client Directive: Component Modules That Consume React State

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all frontend UI components within the documentation and web interface packages requiring interactive state, DOM manipulation, or browser APIs, and integration wrapper components interfacing with client-only third-party UI widgets and search dialogs.

### Rules

- **R-RSC-001** MUST: UI component modules that consume React state hooks, effect hooks, callback hooks, or DOM references MUST declare the use client directive at the module root before any import statements.

### Verify

```bash
# Discover dependency manifest and lock artifact, and verify exact resolved versions
# Discover and run static analysis and linting scripts to verify client hooks are accompanied by client boundary declarations
# Discover and execute build verification command to confirm clean compilation across server and client component boundaries
```

**Accept when:**
- All UI components utilizing React state, effects, browser DOM references, or client-only hooks declare the use client directive at the module root.
- Static and server-renderable UI components without interactivity remain free of the use client directive to avoid unnecessary client bundle growth.
- Automated build and static analysis checks pass with zero client boundary syntax or runtime lifecycle errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification via static analysis, linting, and build verification is mandatory.
</enforcement>