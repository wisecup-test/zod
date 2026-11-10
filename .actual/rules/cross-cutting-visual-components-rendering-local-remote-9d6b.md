---
version: 2
name: cross-cutting-visual-components-rendering-local-remote-9d6b
description: "Adoption of next/image for Optimized UI Image Rendering: Visual Components Rendering Local Remote Raster"
metadata:
  actual:
    adr_id: 9d6b1109-2f2b-4acd-8110-4208d8594bc2
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

# Adoption of next/image for Optimized UI Image Rendering: Visual Components Rendering Local Remote Raster

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-IMG-001** MUST: All visual components rendering local or remote raster graphics and brand logos MUST import and utilize the next/image module for asset presentation.

### Verify

```bash
# Discover and execute the repository linter suite to check for prohibited native image markup in presentation components
# Discover and run the project type-checker and build pipeline to verify that next/image invocations satisfy contract constraints
```

**Accept when:**
- Repository linting rules verify no raw HTML image tags exist within documentation component modules.
- Type verification and build commands succeed with all next/image properties matching resolved module definitions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>