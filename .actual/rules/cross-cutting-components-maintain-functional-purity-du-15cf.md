---
version: 2
name: cross-cutting-components-maintain-functional-purity-du-15cf
description: "Adoption of React as Core UI Component Library: Components Maintain Functional Purity During Rendering"
metadata:
  actual:
    adr_id: 15cfae7e-7c2e-4dfe-98e9-ce03bb74a300
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

# Adoption of React as Core UI Component Library: Components Maintain Functional Purity During Rendering

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation user interface components, layout templates, interactive client widgets, and modules responsible for rendering documentation content, navigation hierarchies, and client dialogs.

### Rules

- **R-ACT-001** SHOULD: Components SHOULD maintain functional purity during rendering by deferring non-rendering side effects to hook lifecycles.

### Verify

```bash
# Discover the repository build script from the dependency manifest and execute the static type verification.
# Inspect project configuration to identify and run the static linter verifying component hook constraints and client directive compliance.
```

**Accept when:**
- All component modules pass static type checking without missing dependency declarations.
- Component lint verification passes with zero violations of hook rules and rendering boundary constraints.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration static analysis, linting, and type-checking suites, as well as architectural review during pull request evaluation.
</enforcement>