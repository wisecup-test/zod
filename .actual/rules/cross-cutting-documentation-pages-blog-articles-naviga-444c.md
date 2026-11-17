---
version: 2
name: cross-cutting-documentation-pages-blog-articles-naviga-444c
description: "Adoption of Shared Internal Module `@/components/inline-code-title` for Code Title Presentation: Documentation Pages Blog Articles Navigation Elements"
metadata:
  actual:
    adr_id: 444c050d-d301-4a8c-8616-5e7a36f5ec2b
    status: accepted
    candidate_group_id: bedfd70d-2d50-4010-8699-3f33e118e97e
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/blog/**
      - components/**
---

# Adoption of Shared Internal Module `@/components/inline-code-title` for Code Title Presentation: Documentation Pages Blog Articles Navigation Elements

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CODE-001** MUST: All documentation pages, blog articles, navigation elements, and syndicated content feeds displaying titled code segments MUST import and render code titles using the shared internal `@/components/inline-code-title` module.

### Verify

```bash
# Discover and execute the repository static analysis script or linter to verify all code title imports resolve to the shared internal component.
# Discover and run the project type checking and test suites to verify interface compatibility across documentation routes and components.
```

**Accept when:**
- All documentation pages, blog views, navigation components, and syndication endpoints import code title rendering from the centralized internal module without unresolved path errors.
- Project static analysis, type verification, and test suites pass without violations regarding unshared inline code title implementations.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests containing ad-hoc code title implementations or unapproved styling wrappers are blocked until updated to import the shared module.
</enforcement>