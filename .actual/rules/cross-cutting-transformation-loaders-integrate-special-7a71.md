---
version: 2
name: cross-cutting-transformation-loaders-integrate-special-7a71
description: "Adoption of @/loaders/source Module for Documentation Source Resolution: Transformation Loaders Integrate Specialized Markdown Middleware"
metadata:
  actual:
    adr_id: 7a710aba-1d40-49b5-b73b-1b06285a47f6
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

# Adoption of @/loaders/source Module for Documentation Source Resolution: Transformation Loaders Integrate Specialized Markdown Middleware

Scope: applies to `packages/docs/app/llms-full.txt/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-SRC-001** MAY: Transformation loaders MAY integrate specialized markdown middleware to augment raw page content prior to serving serialized documentation representations.

### Verify

```bash
# Inspect workspace configuration for project test script and run test suite
# Discover and run project typecheck and linting commands from package manifest
```

**Accept when:**
- Documentation route handlers and text extraction loaders resolve page sources through @/loaders/source without import boundary errors.
- Automated verification suites confirm consistent page order indexing and successful content extraction across all endpoints.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>