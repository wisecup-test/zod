---
version: 2
name: cross-cutting-components-displaying-theme-specific-gra-d42e
description: "Adoption of next/image for Optimized UI Image Rendering: Components Displaying Theme Specific Graphics Encapsulate"
metadata:
  actual:
    adr_id: d42ed304-139f-44fa-88ad-d54b11b47144
    status: accepted
    candidate_group_id: 4180091f-05d3-44bb-80df-872af0ec478d
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
      - components/**
---

# Adoption of next/image for Optimized UI Image Rendering: Components Displaying Theme Specific Graphics Encapsulate

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for:
- All presentation components, layouts, and brand visual elements rendering raster images.
- Client-side and shared layout components displaying logo assets and theme-dependent imagery.

### Rules

- **R-LM-001** SHOULD: Components displaying theme-specific graphics SHOULD encapsulate theme-switching logic within dedicated wrapper components utilizing next/image rather than duplicating inline styling.

### Verify

- Discover and execute the repository linter suite to check for prohibited native image markup in presentation components.
- Discover and run the project type-checker and build pipeline to verify that next/image invocations satisfy contract constraints.

**Accept when:**

- Repository linting rules verify no raw HTML image tags exist within documentation component modules.
- Type verification and build commands succeed with all next/image properties matching resolved module definitions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated linting rules prohibiting native image elements in component files.
- Verified by: Continuous integration type validation and build verification.
- Verified by: Pull request code review of newly introduced visual presentation components.
- Violation handling: Automated continuous integration failure upon detection of unapproved image markup.
- Violation handling: Required refactoring to replace raw tags with next/image before pull request merge.
- Exception process: Submit an exception request to the architecture team specifying the technical constraint precluding next/image adoption.
- Exception process: Obtain documented architectural approval before bypassing linting or merging code.
</enforcement>
