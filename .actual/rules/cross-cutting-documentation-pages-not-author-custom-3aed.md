---
version: 2
name: cross-cutting-documentation-pages-not-author-custom-3aed
description: "Adoption of fumadocs-ui for Documentation Application Layouts: Documentation Pages Not Author Custom Navigation"
metadata:
  actual:
    adr_id: 3aedebad-cef5-44a7-a2a0-bbaa9eb9ec44
    status: accepted
    candidate_group_id: ac811e8d-24b1-44b1-9dc6-e30b8032ba34
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui for Documentation Application Layouts: Documentation Pages Not Author Custom Navigation

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-FUMA-001** MUST_NOT: Documentation pages MUST NOT author custom navigation wrapper shells that bypass the shared documentation layout components.

### Verify

```bash
# Discover and execute the project verification script from the repository manifest to confirm import validity and type consistency across documentation routes.
# Run the repository automated linting check to verify that documentation layouts do not import unapproved layout alternatives.
```

**Accept when:**
- All documentation layout routes import documentation scaffolding components exclusively from the designated documentation UI library.
- Repository verification scripts pass without unresolved module imports or layout contract mismatches.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated linting and architectural peer review verify compliance during pull request validation, and violations block merging.
</enforcement>