---
version: 2
name: cross-cutting-prior-integrating-updating-fumadocs-layo-6e4c
description: "Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Prior Integrating Updating Fumadocs Layout Components"
metadata:
  actual:
    adr_id: 6e4cf82a-7244-4cc2-8212-0298f56e94f5
    status: accepted
    candidate_group_id: 3eda226b-0493-41c6-8697-5bf32b4fdf24
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Prior Integrating Updating Fumadocs Layout Components

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-FUMA-001** MUST: Prior to integrating or updating fumadocs-ui layout components, developers MUST inspect the repository dependency manifest and resolution artifact to resolve the exact locked version and verify API compatibility against official version-specific documentation.

### Verify

```bash
# Discover and execute the project build and static analysis scripts to confirm layout component type conformance
# Discover and execute the project test runner to verify route layout components render with required configuration properties
# Inspect layout imports across documentation route hierarchies to confirm layout components are sourced from fumadocs-ui layout entry points
```

**Accept when:**
- Static type analysis passes with zero errors across all documentation route layout modules.
- Documentation and content route layouts render navigation headers, sidebars, and main content containers without runtime exceptions.
- All route layout implementations ingest the centralized layout configuration module without local duplication of global navigation structures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration checks and peer code review.
</enforcement>