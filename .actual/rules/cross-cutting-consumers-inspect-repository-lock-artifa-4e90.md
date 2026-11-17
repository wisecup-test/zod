---
version: 2
name: cross-cutting-consumers-inspect-repository-lock-artifa-4e90
description: "next/link Client Navigation Module Adoption: Consumers Inspect Repository Lock Artifact Determine"
metadata:
  actual:
    adr_id: 4e90188a-c504-4d38-bf1e-d8fabc1beecc
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

# next/link Client Navigation Module Adoption: Consumers Inspect Repository Lock Artifact Determine

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all page views and interactive UI components requiring navigation between internal application routes.

### Rules

- **R-NAV-001** MUST: Consumers MUST inspect the repository lock artifact to determine the exact installed version of the navigation dependency and verify compatible link properties before implementation.
- **R-NAV-002** MUST: Wrap next/link instances in presentation components when applying design system utility styling or responsive layout rules.
- **R-NAV-003** MUST: Ensure passing appropriate accessibility attributes and destination href values to maintain keyboard navigability and semantic structure.

### Verify

```bash
# Discover and execute repository static analysis and linting scripts to identify non-compliant anchor usage
# Discover and execute repository test runner to verify navigation component rendering and routing integrity
```

**Accept when:**
- All internal navigation hyperlinks render through next/link without unmanaged anchor element fallbacks.
- Repository static analysis and test validation suites pass without routing rule violations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Compliance is verified via static analysis, lint checks, and code reviews in continuous integration pipelines.
</enforcement>