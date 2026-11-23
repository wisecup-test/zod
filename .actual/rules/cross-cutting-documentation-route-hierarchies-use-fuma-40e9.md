---
version: 2
name: cross-cutting-documentation-route-hierarchies-use-fuma-40e9
description: "Adoption of fumadocs-ui for Documentation Application Layouts: Documentation Route Hierarchies Use Fumadocs Layouts"
metadata:
  actual:
    adr_id: 40e99bc8-5d0f-43ed-8217-768cbeeb7d3e
    status: accepted
    candidate_group_id: ac811e8d-24b1-44b1-9dc6-e30b8032ba34
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui for Documentation Application Layouts: Documentation Route Hierarchies Use Fumadocs Layouts

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for:
- All documentation route layouts, content pages, and related status fallback boundaries within the documentation application.

### Rules

- **R-LM-001** MUST: Documentation route hierarchies MUST use fumadocs-ui/layouts/docs and fumadocs-ui/page as the standard structural layout and presentation primitives.

### Verify

- Discover and execute the project verification script from the repository manifest to confirm import validity and type consistency across documentation routes.
- Run the repository automated linting check to verify that documentation layouts do not import unapproved layout alternatives.

**Accept when:**

- All documentation layout routes import documentation scaffolding components exclusively from the designated documentation UI library.
- Repository verification scripts pass without unresolved module imports or layout contract mismatches.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated linting and import boundaries verified during pull request validation.
- Verified by: Architectural peer review of all documentation layout route additions and updates.
- Violation handling: Pull requests introducing ad-hoc documentation layout wrappers without exception approval are blocked from merge.
- Violation handling: Violations identified during code review must be refactored to consume approved documentation UI primitives.
- Exception process: Submit an architectural exception request detailing layout constraints that cannot be satisfied by the documentation UI library.
- Exception process: Obtain documented approval from documentation module maintainers prior to merging custom layout alternatives.
</enforcement>
