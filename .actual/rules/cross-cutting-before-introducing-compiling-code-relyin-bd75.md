---
version: 2
name: cross-cutting-before-introducing-compiling-code-relyin-bd75
description: "Adoption of React as Core UI Component Library: Before Introducing Compiling Code Relying React"
metadata:
  actual:
    adr_id: bd758cae-ba07-4bd4-881b-eff09148593e
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

# Adoption of React as Core UI Component Library: Before Introducing Compiling Code Relying React

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for:
- Documentation user interface components, layout templates, and interactive client widgets.
- Modules responsible for rendering documentation content, navigation hierarchies, and client dialogs.

### Rules

- **R-LM-001** MUST: Before introducing or compiling code relying on React dependencies, developers MUST discover the ecosystem lock artifact and verify the exact resolved library version according to the Discovery Policy.

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
