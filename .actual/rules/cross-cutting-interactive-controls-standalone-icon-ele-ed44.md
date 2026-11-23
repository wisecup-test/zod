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

These rules are ALWAYS ACTIVE for:
- All user interface components, layouts, and documentation views requiring visual icons or glyphs.

### Rules

- **R-LM-001** SHOULD: Interactive controls and standalone icon elements SHOULD supply accessible text labels or assistive attributes for screen readers.

### Verify

- Discover the project verification and linting scripts from the repository manifest and execute them to verify that icon imports adhere to architectural constraints.
- Inspect the dependency resolution lock artifact to confirm that only the approved icon library is resolved without unapproved iconography dependencies.
- Execute the workspace type-checking and build commands to confirm all icon component invocations pass compile-time verification.

**Accept when:**

- All icon references across interface components resolve to imports from the approved icon library.
- Type-checking and static analysis scripts run to completion with zero errors or warnings regarding icon component usage.
- No extraneous icon dependencies or inline SVG glyph duplicates exist within the component tree.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated lint rules and static analysis in continuous integration pipelines checking import paths.
- Verified by: Peer code review verifying adherence to standardized iconography components and styling.
- Violation handling: Pull requests introducing raw SVG iconography or alternative icon packages are blocked until migrated to lucide-react.
- Violation handling: Violations identified during code review require refactoring to use standard lucide-react components.
- Exception process: Exceptions for proprietary trademarks or unique brand assets unavailable in lucide-react require architecture review approval and documentation in an approved asset registry.
</enforcement>
