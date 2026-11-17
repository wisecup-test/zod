---
version: 2
name: cross-cutting-interactive-controls-standalone-icon-ele-ed44
description: "Lucide React Icon Library Adoption: Interactive Controls Standalone Icon Elements Supply"
metadata:
  actual:
    adr_id: ed4492ab-ade8-4e57-afe3-49794abb43b8
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

# Lucide React Icon Library Adoption: Interactive Controls Standalone Icon Elements Supply

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all user interface components, layouts, and documentation views requiring visual icons or glyphs.

### Rules

- **R-ICON-001** SHOULD: Interactive controls and standalone icon elements SHOULD supply accessible text labels or assistive attributes for screen readers.

### Verify

```bash
# Discover the project verification and linting scripts from the repository manifest and execute them
npm test -- --runInBand || yarn test
# Inspect dependency resolution lock to confirm approved icon library usage
# Execute workspace type-checking and build commands
npm run build || yarn build
```

**Accept when:**
- All icon references across interface components resolve to imports from the approved icon library.
- Type-checking and static analysis scripts run to completion with zero errors or warnings regarding icon component usage.
- No extraneous icon dependencies or inline SVG glyph duplicates exist within the component tree.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated lint rules, static analysis, and peer code reviews enforce compliance.
</enforcement>