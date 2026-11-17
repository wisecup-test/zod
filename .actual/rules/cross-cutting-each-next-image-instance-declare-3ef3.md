---
version: 2
name: cross-cutting-each-next-image-instance-declare-3ef3
description: "Adoption of next/image for Optimized UI Image Rendering: Each Next Image Instance Declare Explicit"
metadata:
  actual:
    adr_id: 3ef35e6d-3677-4a44-93cd-97814aa1ecf8
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

# Adoption of next/image for Optimized UI Image Rendering: Each Next Image Instance Declare Explicit

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all presentation components, layouts, and brand visual elements rendering raster images, client-side and shared layout components displaying logo assets and theme-dependent imagery.

### Rules

- **R-IMG-001** MUST: Each next/image instance MUST declare explicit dimension attributes or use container fill properties to maintain layout stability during media loading.

### Verify

```bash
# Discover and execute the repository linter suite to check for prohibited native image markup in presentation components
# Discover and run the project type-checker and build pipeline to verify that next/image invocations satisfy contract constraints
```

**Accept when:**
- Repository linting rules verify no raw HTML image tags exist within documentation component modules.
- Type verification and build commands succeed with all next/image properties matching resolved module definitions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling includes automated continuous integration failure upon detection of unapproved image markup and required refactoring to replace raw tags with next/image before pull request merge.
</enforcement>