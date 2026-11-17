---
version: 2
name: cross-cutting-documentation-routes-content-utilities-n-46bf
description: "Adoption of @/loaders/source Module for Documentation Source Resolution: Documentation Routes Content Utilities Not Bypass"
metadata:
  actual:
    adr_id: 46bf3c15-1c89-4fc4-9599-36b61ebff085
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

# Adoption of @/loaders/source Module for Documentation Source Resolution: Documentation Routes Content Utilities Not Bypass

Scope: applies to `packages/docs/app/llms-full.txt/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation route handlers and content utilities.

### Rules

- **R-SRC-001** MUST_NOT: Documentation routes and content utilities MUST NOT bypass the centralized source loader to implement ad-hoc file reading or independent page source compilation.

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