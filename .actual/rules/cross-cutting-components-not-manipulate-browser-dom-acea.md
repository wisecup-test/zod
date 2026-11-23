---
version: 2
name: cross-cutting-components-not-manipulate-browser-dom-acea
description: "Adoption of React as Core UI Component Library: Components Not Manipulate Browser Dom Directly"
metadata:
  actual:
    adr_id: acea78a8-d583-4237-b158-7b42bbc318fe
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

# Adoption of React as Core UI Component Library: Components Not Manipulate Browser Dom Directly

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for:
- Documentation user interface components, layout templates, and interactive client widgets.
- Modules responsible for rendering documentation content, navigation hierarchies, and client dialogs.

### Rules

- **R-LM-001** MUST_NOT: Components MUST_NOT manipulate the browser DOM directly unless coordinated through React references.

### Verify

- Discover the repository build script from the dependency manifest and execute the static type verification.
- Inspect project configuration to identify and run the static linter verifying component hook constraints and client directive compliance.

**Accept when:**

- All component modules pass static type checking without missing dependency declarations.
- Component lint verification passes with zero violations of hook rules and rendering boundary constraints.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration static analysis, linting, and type-checking suites.
- Verified by: Architectural review during pull request evaluation to verify component boundaries and hook lifecycles.
- Violation handling: Pull requests introducing direct DOM manipulation outside references or omitting required rendering boundaries are blocked until remediated.
- Exception process: Exceptions require documented architectural justification and formal approval from the engineering team leads.
</enforcement>
