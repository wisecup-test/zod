---
version: 2
name: cross-cutting-route-layout-components-not-implement-5fd7
description: "Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Route Layout Components Not Implement Custom"
metadata:
  actual:
    adr_id: 5fd7e651-a21f-4209-94c9-bd501c88df4e
    status: accepted
    candidate_group_id: 3eda226b-0493-41c6-8697-5bf32b4fdf24
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Route Layout Components Not Implement Custom

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-FUMA-001** MUST_NOT: Route layout components MUST NOT implement custom sidebar navigation drawers or responsive menu toggle logic that bypasses or conflicts with fumadocs-ui layout state management.

### Verify

```bash
# Discover the project manifest and execute type-checking pipeline
# Discover and execute project test runner
# Inspect layout imports across documentation route hierarchies
```

**Accept when:**
- Static type analysis passes with zero errors across all documentation route layout modules.
- Documentation and content route layouts render navigation headers, sidebars, and main content containers without runtime exceptions.
- All route layout implementations ingest the centralized layout configuration module without local duplication of global navigation structures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is enforced via automated continuous integration checks executing static type analysis, application build verification, and peer code review.
</enforcement>