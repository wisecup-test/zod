---
version: 2
name: cross-cutting-downstream-transformation-pipelines-cons-878f
description: "Adoption of @/loaders/source Module for Documentation Source Resolution: Downstream Transformation Pipelines Consume Canonical Page"
metadata:
  actual:
    adr_id: 878f5b30-cebc-43ff-87dd-326485d32b28
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

# Adoption of @/loaders/source Module for Documentation Source Resolution: Downstream Transformation Pipelines Consume Canonical Page

Scope: applies to `packages/docs/app/llms-full.txt/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-SRC-001** SHOULD: Downstream transformation pipelines SHOULD consume canonical page objects emitted by @/loaders/source and isolate formatting transformations within dedicated loader utilities.

### Verify

```bash
# Inspect the workspace configuration to discover the project verification script, then run the test suite to validate documentation loader resolution.
# Discover and run the project typecheck and linting commands from the package manifest to verify import boundary compliance across documentation endpoints.
```

**Accept when:**
- Documentation route handlers and text extraction loaders resolve page sources through @/loaders/source without import boundary errors.
- Automated verification suites confirm consistent page order indexing and successful content extraction across all endpoints.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>