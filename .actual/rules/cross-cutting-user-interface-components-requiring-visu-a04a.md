---
version: 2
name: cross-cutting-user-interface-components-requiring-visu-a04a
description: "Lucide React Icon Library Adoption: User Interface Components Requiring Visual Iconography"
metadata:
  actual:
    adr_id: a04a9096-999d-4c8b-bc77-e1b989c5a9c4
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

# Lucide React Icon Library Adoption: User Interface Components Requiring Visual Iconography

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-LUCIDE-001** MUST: User interface components requiring visual iconography MUST import icon components exclusively from lucide-react.

### Verify

```bash
# Discover and execute project linting, type-checking, and build scripts from the repository manifest
# to verify icon imports adhere to architectural constraints and pass compile-time verification.
```

**Accept when:**
- All icon references across interface components resolve to imports from the approved icon library (`lucide-react`).
- Type-checking and static analysis scripts run to completion with zero errors or warnings regarding icon component usage.
- No extraneous icon dependencies or inline SVG glyph duplicates exist within the component tree, except where approved via exception (e.g., EXC-20-001).

<enforcement>
Claude Code MUST NOT skip or defer verification. All icon imports must be validated via automated lint rules, static analysis, and type checking.
</enforcement>