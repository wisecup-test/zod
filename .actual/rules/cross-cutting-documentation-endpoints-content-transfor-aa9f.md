---
version: 2
name: cross-cutting-documentation-endpoints-content-transfor-aa9f
description: "Adoption of @/loaders/source Module for Documentation Source Resolution: Documentation Endpoints Content Transformation Loaders Resolve"
metadata:
  actual:
    adr_id: aa9fbf1d-77b8-4e04-9e60-a7e88cbffba7
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

# Adoption of @/loaders/source Module for Documentation Source Resolution: Documentation Endpoints Content Transformation Loaders Resolve

Scope: applies to `packages/docs/app/llms-full.txt/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation route handlers, documentation loader utilities, and content transformation pipelines that query or compile documentation pages.

### Rules

- **R-SRC-001** MUST: All documentation endpoints and content transformation loaders MUST resolve documentation page collections, navigation trees, and metadata through the centralized @/loaders/source module.

### Verify

```bash
# Inspect the workspace configuration to discover the project verification script, then run the test suite to validate documentation loader resolution.
# Discover and run the project typecheck and linting commands from the package manifest to verify import boundary compliance across documentation endpoints.
```

**Accept when:**
- Documentation route handlers and text extraction loaders resolve page sources through @/loaders/source without import boundary errors.
- Automated verification suites confirm consistent page order indexing and successful content extraction across all endpoints.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests containing direct filesystem access or bypasses of the source loader are rejected until refactored to use @/loaders/source.
</enforcement>