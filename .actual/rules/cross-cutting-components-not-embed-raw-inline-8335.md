---
version: 2
name: cross-cutting-components-not-embed-raw-inline-8335
description: "Lucide React Icon Library Adoption: Components Not Embed Raw Inline Svg"
metadata:
  actual:
    adr_id: 833548ab-092c-4bf8-9fd5-c22e47ee450a
    status: accepted
    candidate_group_id: baac6196-67d6-42bf-b224-b08a619e635d
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
      - components/**
      - loaders/**
---

# Lucide React Icon Library Adoption: Components Not Embed Raw Inline Svg

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all user interface components, layouts, and documentation views requiring visual icons or glyphs.

### Rules

- **R-LUC-001** MUST_NOT: Components MUST NOT embed raw inline SVG markup for iconography supported by the adopted icon library or introduce secondary third-party icon packages.

### Verify

```bash
# Discover and execute project verification and linting scripts from the repository manifest
# Inspect the dependency resolution lock artifact to confirm only approved icon libraries are resolved
# Execute workspace type-checking and build commands
```

**Accept when:**
- All icon references across interface components resolve to imports from the approved icon library.
- Type-checking and static analysis scripts run to completion with zero errors or warnings regarding icon component usage.
- No extraneous icon dependencies or inline SVG glyph duplicates exist within the component tree.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>