---
version: 2
name: cross-cutting-content-rendering-components-not-define-3974
description: "Adoption of Shared Internal Module `@/components/inline-code-title` for Code Title Presentation: Content Rendering Components Not Define Hoc"
metadata:
  actual:
    adr_id: 3974e063-02d7-489a-85b0-bb604376b637
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

# Adoption of Shared Internal Module `@/components/inline-code-title` for Code Title Presentation: Content Rendering Components Not Define Hoc

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for:
- Documentation content pages, blog rendering views, navigation sidebars, and syndicated feed endpoints that display code titles.
- UI components within the documentation workspace requiring standardized code title labels.

### Rules

- **R-LM-001** MUST_NOT: Content rendering components MUST NOT define ad-hoc, inline, or unshared structural wrappers for code snippet titles.

### Verify

- Discover and execute the repository static analysis script to verify all code title imports resolve to the shared internal component.
- Discover and run the project type checking and test suites to verify interface compatibility across documentation routes and components.

**Accept when:**

- All documentation pages, blog views, navigation components, and syndication endpoints import code title rendering from the centralized internal module without unresolved path errors.
- Project static analysis, type verification, and test suites pass without violations regarding unshared inline code title implementations.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis and linter rules checking import statements during continuous integration.
- Verified by: Peer code review for all new documentation components, blog templates, and feed generation routes.
- Violation handling: Pull requests containing ad-hoc code title implementations or unapproved styling wrappers are blocked until updated to import the shared module.
- Exception process: Exceptions must be submitted via an architecture review request detailing why the centralized module cannot accommodate the specific presentation or serialization constraint.
</enforcement>
