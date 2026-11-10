---
version: 2
name: cross-cutting-content-transformation-pipelines-registe-1653
description: "Remark Middleware Pipeline Adoption for Content Transformation: Content Transformation Pipelines Register Middleware Sequential"
metadata:
  actual:
    adr_id: 1653d73a-cf08-4535-83c1-97b22bfd049f
    status: accepted
    candidate_group_id: 30f8ed46-ca19-4914-926e-132a5ad326d6
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - loaders/**
---

# Remark Middleware Pipeline Adoption for Content Transformation: Content Transformation Pipelines Register Middleware Sequential

Scope: applies to `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation loader modules transforming Markdown and MDX content and text extraction pipelines preparing documentation content for downstream ingestion.

### Rules

- **R-TRANS-001** MUST: Content transformation pipelines MUST register middleware in sequential order using remark().use(remarkMdx).use(remarkInclude).use(remarkGfm).use(remarkStringify) to ensure proper syntax parsing, transclusion, and output serialization.

### Verify

```bash
# Discover and execute the project test runner covering documentation loaders
# Discover the static analysis command and verify loader pipeline definitions
```

**Accept when:**
- The documentation loader pipeline successfully parses MDX sources and produces valid string representations.
- All automated test suites and static analysis checks covering document extraction execute without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>