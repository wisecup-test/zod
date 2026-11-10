---
version: 2
name: cross-cutting-before-introducing-updating-dependencies-c60d
description: "Adoption of @/loaders/source Module for Documentation Source Resolution: Before Introducing Updating Dependencies That Integrate"
metadata:
  actual:
    adr_id: c60d716e-2c2d-4649-92f0-b9904ac4bbc3
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

# Adoption of @/loaders/source Module for Documentation Source Resolution: Before Introducing Updating Dependencies That Integrate

Scope: applies to `packages/docs/app/llms-full.txt/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation route handlers, documentation loader utilities, and transformation pipelines.

### Rules

- **R-SRC-001** MUST: Before introducing or updating dependencies that integrate with the documentation source loader, the engineering team MUST inspect the repository lock artifact to determine and verify the exact resolved version.

### Verify

```bash
# Inspect the workspace configuration to discover the project verification script, then run tests and typechecks
npm test
npm run typecheck
npm run lint
```

**Accept when:**
- Documentation route handlers and text extraction loaders resolve page sources through @/loaders/source without import boundary errors.
- Automated verification suites confirm consistent page order indexing and successful content extraction across all endpoints.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>