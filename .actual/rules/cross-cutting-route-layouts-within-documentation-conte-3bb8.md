---
version: 2
name: cross-cutting-route-layouts-within-documentation-conte-3bb8
description: "Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Route Layouts Within Documentation Content Publishing"
metadata:
  actual:
    adr_id: 3bb83262-de3f-4e21-af4f-202cb82ecf49
    status: accepted
    candidate_group_id: 3eda226b-0493-41c6-8697-5bf32b4fdf24
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Route Layouts Within Documentation Content Publishing

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DOC-001** MUST: Route layouts within documentation and content publishing application segments MUST use fumadocs-ui layout primitives to structure header, sidebar, and content container presentation.

### Verify

```bash
# Discover and execute project type-checking and build verification scripts from the project manifest
# Example: pnpm check / npm run build
```

**Accept when:**
- Static type analysis passes with zero errors across all documentation route layout modules.
- Documentation and content route layouts render navigation headers, sidebars, and main content containers without runtime exceptions.
- All route layout implementations ingest the centralized layout configuration module without local duplication of global navigation structures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks execute static type analysis and application build verification.
</enforcement>