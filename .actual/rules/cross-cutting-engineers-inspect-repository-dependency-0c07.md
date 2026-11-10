---
version: 2
name: cross-cutting-engineers-inspect-repository-dependency-0c07
description: "Adoption of next/image for Optimized UI Image Rendering: Engineers Inspect Repository Dependency Manifest Authoritative"
metadata:
  actual:
    adr_id: 0c07c1b2-fadb-4579-a5aa-9d1ddda8bba6
    status: accepted
    candidate_group_id: 4180091f-05d3-44bb-80df-872af0ec478d
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
      - components/**
---

# Adoption of next/image for Optimized UI Image Rendering: Engineers Inspect Repository Dependency Manifest Authoritative

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-IMG-001** MUST: Engineers MUST inspect the repository dependency manifest and authoritative lock artifact to ground the resolved next/image module version against official API documentation before implementing image components.

### Verify

```bash
# Discover and execute the repository linter suite to check for prohibited native image markup in presentation components
# Discover and run the project type-checker and build pipeline to verify that next/image invocations satisfy contract constraints
```

**Accept when:**
- Repository linting rules verify no raw HTML image tags exist within documentation component modules.
- Type verification and build commands succeed with all next/image properties matching resolved module definitions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>