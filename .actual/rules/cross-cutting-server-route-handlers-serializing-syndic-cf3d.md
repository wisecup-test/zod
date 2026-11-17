---
version: 2
name: cross-cutting-server-route-handlers-serializing-syndic-cf3d
description: "Adoption of Shared Internal Module `@/components/inline-code-title` for Code Title Presentation: Server Route Handlers Serializing Syndicated Content"
metadata:
  actual:
    adr_id: cf3da65f-b128-480e-bc0c-077019108fb3
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

# Adoption of Shared Internal Module `@/components/inline-code-title` for Code Title Presentation: Server Route Handlers Serializing Syndicated Content

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ADR-001** MAY: Server route handlers serializing syndicated content MAY pass plain text projections derived from `@/components/inline-code-title` when markup serialization is restricted.

### Verify

```bash
# Discover and execute the repository static analysis script to verify all code title imports resolve to the shared internal component.
# Discover and run the project type checking and test suites to verify interface compatibility across documentation routes and components.
```

**Accept when:**
- All documentation pages, blog views, navigation components, and syndication endpoints import code title rendering from the centralized internal module without unresolved path errors.
- Project static analysis, type verification, and test suites pass without violations regarding unshared inline code title implementations.

<enforcement>
Claude Code MUST NOT skip or defer verification. All documentation components, blog templates, and feed generation routes are verified by automated static analysis and peer code review.
</enforcement>