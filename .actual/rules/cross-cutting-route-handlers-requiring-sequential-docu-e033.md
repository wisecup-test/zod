---
version: 2
name: cross-cutting-route-handlers-requiring-sequential-docu-e033
description: "Adoption of @/loaders/source Module for Documentation Source Resolution: Route Handlers Requiring Sequential Document Navigation"
metadata:
  actual:
    adr_id: e033ccab-11ba-47aa-846d-49a4c9763559
    status: accepted
    candidate_group_id: 9d555df3-dbda-4668-b9e0-8bc90459cc7b
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/llms-full.txt/**
      - loaders/**
---

# Adoption of @/loaders/source Module for Documentation Source Resolution: Route Handlers Requiring Sequential Document Navigation

Scope: applies to `packages/docs/app/llms-full.txt/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation route handlers and text extraction loaders that interface with documentation source pages or frontmatter.

### Rules

- **R-SRC-001** SHOULD: Route handlers requiring sequential document navigation SHOULD maintain an indexed lookup cache derived from source loader collections to ensure constant-time page ordering.

### Verify

```bash
# Discover and run the project typecheck, linting, and test suite to validate documentation loader resolution
# (Inspect workspace configuration/package manifest for actual commands)
npm test
npm run typecheck
npm run lint
```

**Accept when:**
- Documentation route handlers and text extraction loaders resolve page sources through @/loaders/source without import boundary errors.
- Automated verification suites confirm consistent page order indexing and successful content extraction across all endpoints.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests containing direct filesystem access or bypasses of the source loader are rejected until refactored to use @/loaders/source.
</enforcement>