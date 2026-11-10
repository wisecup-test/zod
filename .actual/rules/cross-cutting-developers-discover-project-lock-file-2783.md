---
version: 2
name: cross-cutting-developers-discover-project-lock-file-2783
description: "Adoption of fumadocs-ui for Documentation Application Layouts: Developers Discover Project Lock File Resolve"
metadata:
  actual:
    adr_id: 2783b813-03db-4bb1-812f-5dfcc48c6d03
    status: accepted
    candidate_group_id: ac811e8d-24b1-44b1-9dc6-e30b8032ba34
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui for Documentation Application Layouts: Developers Discover Project Lock File Resolve

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-FUMA-001** MUST: Developers MUST discover the project lock file and resolve the exact installed version of the documentation library before introducing or modifying layout implementations.

### Verify

```bash
# Discover and execute the project verification script from the repository manifest to confirm import validity and type consistency across documentation routes.
# Run the repository automated linting check to verify that documentation layouts do not import unapproved layout alternatives.
```

**Accept when:**
- All documentation layout routes import documentation scaffolding components exclusively from the designated documentation UI library.
- Repository verification scripts pass without unresolved module imports or layout contract mismatches.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated linting and architectural peer review verify compliance during pull request validation; violations are blocked from merge.
</enforcement>