---
version: 2
name: cross-cutting-components-not-render-standard-html-9f07
description: "Adoption of next/image for Optimized UI Image Rendering: Components Not Render Standard Html Img"
metadata:
  actual:
    adr_id: 9f07cf2f-7d43-4b12-b7fd-974ce5917027
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

# Adoption of next/image for Optimized UI Image Rendering: Components Not Render Standard Html Img

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-IMG-001** MUST_NOT: Components MUST NOT render standard HTML img elements for static or remote media assets within the presentation layer.

### Verify

```bash
# Discover and execute the repository linter suite and type-checker/build pipeline
```

**Accept when:**
- Repository linting rules verify no raw HTML image tags exist within documentation component modules.
- Type verification and build commands succeed with all next/image properties matching resolved module definitions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated linting, CI type validation, build verification, and pull request code review.
</enforcement>