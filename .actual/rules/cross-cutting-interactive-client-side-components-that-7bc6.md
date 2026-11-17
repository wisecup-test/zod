---
version: 2
name: cross-cutting-interactive-client-side-components-that-7bc6
description: "Adoption of React as Core UI Component Library: Interactive Client Side Components That Invoke"
metadata:
  actual:
    adr_id: 7bc6e2ca-e2af-4c7d-b92c-65eab088e9ba
    status: accepted
    candidate_group_id: b06f414d-38f9-4b85-bef7-5ca278d92919
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
      - components/**
      - loaders/**
---

# Adoption of React as Core UI Component Library: Interactive Client Side Components That Invoke

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation user interface components, layout templates, interactive client widgets, and modules responsible for rendering documentation content, navigation hierarchies, and client dialogs.

### Rules

- **R-ACT-001** MUST: Interactive client-side components that invoke React hooks or register DOM event handlers MUST explicitly declare the client component rendering boundary directive at the top of the module.

### Verify

```bash
# Discover the repository build script from the dependency manifest and execute static type verification.
# Inspect project configuration to identify and run the static linter verifying component hook constraints and client directive compliance.
```

**Accept when:**
- All component modules pass static type checking without missing dependency declarations.
- Component lint verification passes with zero violations of hook rules and rendering boundary constraints.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>