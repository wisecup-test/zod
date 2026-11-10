---
version: 2
name: cross-cutting-documentation-text-transformation-loader-b653
description: "Remark Middleware Pipeline Adoption for Content Transformation: Documentation Text Transformation Loaders Processing Markdown"
metadata:
  actual:
    adr_id: b6533567-b53c-492d-92f3-951d91640644
    status: accepted
    candidate_group_id: 30f8ed46-ca19-4914-926e-132a5ad326d6
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - loaders/**
---

# Remark Middleware Pipeline Adoption for Content Transformation: Documentation Text Transformation Loaders Processing Markdown

Scope: applies to `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation loader modules transforming Markdown and MDX content and text extraction pipelines preparing documentation content for downstream ingestion.

### Rules

- **R-REM-001** MUST: Documentation and text transformation loaders processing Markdown or MDX content MUST assemble transformation pipelines using remark with chained middleware plugin attachments.
- **R-REM-002** MANDATORY: Prior to writing code that uses a versioned library, discover the dependency manifest, identify the build tool, inspect the repository lock or resolution artifact for exact resolved versions, look up official documentation for that exact version, confirm every API/class/function exists in that exact version, and re-run version checks per dependency at point of use.
- **R-REM-003** MANDATORY: Assemble the remark pipeline builder once or configure a reusable loader helper rather than reinstantiating processor chains inside tight iteration loops.
- **R-REM-004** MANDATORY: Ensure plugins that modify the abstract syntax tree structure precede remarkStringify to prevent unparsed syntax leaking into the generated output.
- **R-REM-005** MANDATORY: Verify exact resolved lockfile versions for the unified processor and all registered plugins prior to deployment to prevent runtime pipeline initialization failures.
- **R-REM-006** MANDATORY: Implement recursion depth bounds and cycle detection in document include configurations to prevent circular file transclusion during recursive include resolution via remarkInclude.

### Verify

```bash
# Discover and execute the project test runner covering documentation loaders
# (Derived from dependency manifest in the repository)

# Discover and execute static analysis checks covering loader pipeline definitions
# (Derived from root project configuration in the repository)
```

**Accept when:**
- The documentation loader pipeline successfully parses MDX sources and produces valid string representations.
- All automated test suites and static analysis checks covering document extraction execute without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration checks and peer code reviews.
</enforcement>