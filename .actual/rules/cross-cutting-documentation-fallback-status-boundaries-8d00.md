---
version: 2
name: cross-cutting-documentation-fallback-status-boundaries-8d00
description: "Adoption of fumadocs-ui for Documentation Application Layouts: Documentation Fallback Status Boundaries Within Route"
metadata:
  actual:
    adr_id: 8d00d28f-6669-4487-a338-6c60e989417b
    status: accepted
    candidate_group_id: ac811e8d-24b1-44b1-9dc6-e30b8032ba34
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui for Documentation Application Layouts: Documentation Fallback Status Boundaries Within Route

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for all documentation route layouts, content pages, and related status fallback boundaries within the documentation application.

### Rules

- **R-DOC-001** SHOULD: Documentation fallback and status boundaries within the documentation route tree SHOULD align their presentation tokens with the documentation UI theme tokens.

### Verify

```bash
# Discover and execute the project verification script from the repository manifest to confirm import validity and type consistency across documentation routes.
# Run the repository automated linting check to verify that documentation layouts do not import unapproved layout alternatives.
```

**Accept when:**
- All documentation layout routes import documentation scaffolding components exclusively from the designated documentation UI library.
- Repository verification scripts pass without unresolved module imports or layout contract mismatches.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>