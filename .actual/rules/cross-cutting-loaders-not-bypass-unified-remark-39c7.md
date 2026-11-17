---
version: 2
name: cross-cutting-loaders-not-bypass-unified-remark-39c7
description: "Remark Middleware Pipeline Adoption for Content Transformation: Loaders Not Bypass Unified Remark Abstract"
metadata:
  actual:
    adr_id: 39c7e236-c980-40a9-af38-41a2e01cee2c
    status: accepted
    candidate_group_id: 30f8ed46-ca19-4914-926e-132a5ad326d6
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - loaders/**
---

# Remark Middleware Pipeline Adoption for Content Transformation: Loaders Not Bypass Unified Remark Abstract

Scope: applies to `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation loader modules transforming Markdown and MDX content and text extraction pipelines preparing documentation content for downstream ingestion.

### Rules

- **R-REM-001** MUST_NOT: Loaders MUST_NOT bypass the unified remark abstract syntax tree pipeline with ad-hoc regular expressions or string replacements when resolving includes or stripping markdown formatting.

### Verify

```bash
# Discover and run the project test runner invocation covering documentation loaders
# Discover and run the static analysis command from the root project configuration
```

**Accept when:**
- The documentation loader pipeline successfully parses MDX sources and produces valid string representations.
- All automated test suites and static analysis checks covering document extraction execute without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests modifying documentation parsing or loader pipelines are verified by automated continuous integration checks and peer code review.
</enforcement>