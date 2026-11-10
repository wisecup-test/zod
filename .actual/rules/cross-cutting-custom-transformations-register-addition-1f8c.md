---
version: 2
name: cross-cutting-custom-transformations-register-addition-1f8c
description: "Remark Middleware Pipeline Adoption for Content Transformation: Custom Transformations Register Additional Syntax Plugins"
metadata:
  actual:
    adr_id: 1f8c1e13-72aa-4df9-a099-cc0fda07b511
    status: accepted
    candidate_group_id: 30f8ed46-ca19-4914-926e-132a5ad326d6
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - loaders/**
---

# Remark Middleware Pipeline Adoption for Content Transformation: Custom Transformations Register Additional Syntax Plugins

Scope: applies to `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation loader modules transforming Markdown and MDX content, and text extraction pipelines preparing documentation content for downstream ingestion.

### Rules

- **R-TRANS-001** MAY: Custom transformations MAY register additional syntax plugins after remarkGfm provided they preserve compatibility with remarkStringify.

### Verify

```bash
# Discover and execute the project test runner covering documentation loaders
# Discover and execute the static analysis command from root project configuration
```

**Accept when:**
- The documentation loader pipeline successfully parses MDX sources and produces valid string representations.
- All automated test suites and static analysis checks covering document extraction execute without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks, peer code review, and static analysis verification are mandatory.
</enforcement>