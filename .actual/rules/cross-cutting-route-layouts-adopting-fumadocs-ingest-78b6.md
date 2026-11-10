---
version: 2
name: cross-cutting-route-layouts-adopting-fumadocs-ingest-78b6
description: "Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Route Layouts Adopting Fumadocs Ingest Shared"
metadata:
  actual:
    adr_id: 78b67f20-7774-4b31-91b8-54ec6e4f07eb
    status: accepted
    candidate_group_id: 3eda226b-0493-41c6-8697-5bf32b4fdf24
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Route Layouts Adopting Fumadocs Ingest Shared

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-FUM-001** MUST: Route layouts adopting fumadocs-ui MUST ingest shared navigation, brand identity, and structural options through a centralized layout configuration module rather than declaring local inline navigation schemas.

### Verify

```bash
# Discover the project manifest and execute the type-checking pipeline
# Discover and execute the project test runner
# Inspect layout imports across documentation route hierarchies to confirm layout components are sourced from fumadocs-ui layout entry points
```

**Accept when:**
- Static type analysis passes with zero errors across all documentation route layout modules.
- Documentation and content route layouts render navigation headers, sidebars, and main content containers without runtime exceptions.
- All route layout implementations ingest the centralized layout configuration module without local duplication of global navigation structures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks execute static type analysis and application build verification. Pull requests that implement custom layout shells for documentation or blog routes without utilizing fumadocs-ui layout primitives or an approved exception will be blocked from merging.
</enforcement>