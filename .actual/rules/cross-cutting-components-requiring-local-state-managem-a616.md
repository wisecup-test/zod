---
version: 2
name: cross-cutting-components-requiring-local-state-managem-a616
description: "Adoption of React as Core UI Component Library: Components Requiring Local State Management Browser"
metadata:
  actual:
    adr_id: a616730c-c8e0-422c-8347-e87ccb11ea8e
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

# Adoption of React as Core UI Component Library: Components Requiring Local State Management Browser

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation user interface components, layout templates, interactive client widgets, and modules responsible for rendering documentation content, navigation hierarchies, and client dialogs.

### Rules

- **R-REACT-001** MUST: Components requiring local state management or browser lifecycle coordination MUST encapsulate state transitions through React hooks.

### Verify

```bash
# Discover the repository build script from the dependency manifest and execute the static type verification.
# Inspect project configuration to identify and run the static linter verifying component hook constraints and client directive compliance.
```

**Accept when:**
- All component modules pass static type checking without missing dependency declarations.
- Component lint verification passes with zero violations of hook rules and rendering boundary constraints.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>