---
version: 2
name: cross-cutting-documentation-sub-routes-displaying-tech-f03e
description: "Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Documentation Sub Routes Displaying Technical Reference"
metadata:
  actual:
    adr_id: f03e021f-49bb-4f65-8471-8faa3f7cc180
    status: accepted
    candidate_group_id: 3eda226b-0493-41c6-8697-5bf32b4fdf24
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Documentation Sub Routes Displaying Technical Reference

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-FUMADOCS-001** SHOULD: Documentation sub-routes displaying technical reference material SHOULD use the specialized documentation layout component from fumadocs-ui to provide structured hierarchical navigation and table-of-contents tracking.

### Verify

```bash
# Discover and run the project's build and type-checking pipeline as declared in the manifest
# Example: pnpm build / npm run build / yarn build
# Example: pnpm tsc --noEmit
```

**Accept when:**
- Static type analysis passes with zero errors across all documentation route layout modules.
- Documentation and content route layouts render navigation headers, sidebars, and main content containers without runtime exceptions.
- All route layout implementations ingest the centralized layout configuration module without local duplication of global navigation structures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration checks executing static type analysis and application build verification, backed by peer code review.
</enforcement>