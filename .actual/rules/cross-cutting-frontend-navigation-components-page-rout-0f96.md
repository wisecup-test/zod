---
version: 2
name: cross-cutting-frontend-navigation-components-page-rout-0f96
description: "next/link Client Navigation Module Adoption: Frontend Navigation Components Page Routing Elements"
metadata:
  actual:
    adr_id: 0f96d8f9-6979-46c7-9651-a420c16b0e73
    status: accepted
    candidate_group_id: 8497fb63-f882-4406-98b2-b60281fa558a
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/blog/**
      - components/**
---

# next/link Client Navigation Module Adoption: Frontend Navigation Components Page Routing Elements

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-NAV-001** MUST: Frontend navigation components and page routing elements MUST use the next/link component for all internal hyperlinking to enable client-side route transitions and prefetching.

### Verify

```bash
# Discover and execute the repository static analysis and linting scripts to identify non-compliant anchor usage.
# Discover and execute the repository test runner to verify navigation component rendering and routing integrity.
```

**Accept when:**
- All internal navigation hyperlinks render through next/link without unmanaged anchor element fallbacks.
- Repository static analysis and test validation suites pass without routing rule violations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Static analysis, lint checks, and code reviews enforce these requirements, resulting in build failures or review rejections upon violation.
</enforcement>