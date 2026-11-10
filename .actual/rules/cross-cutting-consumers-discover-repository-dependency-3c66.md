---
version: 2
name: cross-cutting-consumers-discover-repository-dependency-3c66
description: "Lucide React Icon Library Adoption: Consumers Discover Repository Dependency Manifest Resolution"
metadata:
  actual:
    adr_id: 3c6637c2-a361-4c39-bd85-764b96f9ad53
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

# Lucide React Icon Library Adoption: Consumers Discover Repository Dependency Manifest Resolution

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all user interface components, layouts, and documentation views requiring visual icons or glyphs.

### Rules

- **R-LUC-001** MUST: Consumers MUST discover the repository dependency manifest and resolution lock artifact to resolve the exact locked version of lucide-react before implementing icon components.

### Verify

```bash
# Discover the project verification and linting scripts from the repository manifest and execute them to verify that icon imports adhere to architectural constraints.
# Inspect the dependency resolution lock artifact to confirm that only the approved icon library is resolved without unapproved iconography dependencies.
# Execute the workspace type-checking and build commands to confirm all icon component invocations pass compile-time verification.
```

**Accept when:**
- All icon references across interface components resolve to imports from the approved icon library.
- Type-checking and static analysis scripts run to completion with zero errors or warnings regarding icon component usage.
- No extraneous icon dependencies or inline SVG glyph duplicates exist within the component tree.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>