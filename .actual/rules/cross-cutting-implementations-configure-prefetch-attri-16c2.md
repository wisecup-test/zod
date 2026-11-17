---
version: 2
name: cross-cutting-implementations-configure-prefetch-attri-16c2
description: "next/link Client Navigation Module Adoption: Implementations Configure Prefetch Attributes Next Link"
metadata:
  actual:
    adr_id: 16c2caa7-53ea-4c96-84f3-c5cf6538045b
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

# next/link Client Navigation Module Adoption: Implementations Configure Prefetch Attributes Next Link

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all page views, interactive UI components, and internal routing logic.

### Rules

- **R-NXL-001** MAY: Implementations MAY configure prefetch attributes on next/link instances to optimize route transition latency based on viewport visibility.

### Verify

```bash
# Discover and execute the repository static analysis and linting scripts to identify non-compliant anchor usage.
# Discover and execute the repository test runner to verify navigation component rendering and routing integrity.
```

**Accept when:**
- All internal navigation hyperlinks render through next/link without unmanaged anchor element fallbacks.
- Repository static analysis and test validation suites pass without routing rule violations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Compliance is verified by static analysis, lint checks, and code reviews in continuous integration pipelines.
</enforcement>