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

These rules are ALWAYS ACTIVE for all presentation components, layouts, and brand visual elements rendering raster images.

### Rules

- **R-IMG-001** SHOULD: Components displaying theme-specific graphics encapsulate theme-switching logic within dedicated wrapper components utilizing next/image rather than duplicating inline styling.

### Verify

```bash
# Discover and execute the repository linter suite to check for prohibited native image markup in presentation components
npm run lint
# Discover and run the project type-checker and build pipeline to verify that next/image invocations satisfy contract constraints
npm run build
```

**Accept when:**
- Repository linting rules verify no raw HTML image tags exist within documentation component modules.
- Type verification and build commands succeed with all next/image properties matching resolved module definitions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration failure occurs upon detection of unapproved image markup.
</enforcement>