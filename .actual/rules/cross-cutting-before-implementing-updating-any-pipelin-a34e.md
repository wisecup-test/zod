---
version: 2
name: cross-cutting-before-implementing-updating-any-pipelin-a34e
description: "Remark Middleware Pipeline Adoption for Content Transformation: Before Implementing Updating Any Pipeline Component"
metadata:
  actual:
    adr_id: a34e732d-6ac5-4d9b-9096-763014ebede1
    status: accepted
    candidate_group_id: 30f8ed46-ca19-4914-926e-132a5ad326d6
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - loaders/**
---

# Remark Middleware Pipeline Adoption for Content Transformation: Before Implementing Updating Any Pipeline Component

Scope: applies to `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for documentation loader modules transforming Markdown and MDX content and text extraction pipelines preparing documentation content for downstream ingestion.

### Rules

- **R-REM-001** MUST: Before implementing or updating any pipeline component, the consumer MUST inspect the repository lock artifact to determine the exact resolved versions of remark and all registered plugins.
- **R-REM-002** MANDATORY: Execute the lock-version grounding process in order (find dependency manifest, identify build tool, inspect repository lock/resolution artifact, look up official documentation for that exact version, confirm every API/class/function exists in that version, re-run per dependency at point of use) before writing code that uses a versioned library.
- **R-REM-003** MANDATORY: Assemble the remark pipeline builder once or configure a reusable loader helper rather than reinstantiating processor chains inside tight iteration loops.
- **R-REM-004** MANDATORY: Ensure plugins that modify the abstract syntax tree structure precede remarkStringify to prevent unparsed syntax leaking into the generated output.

### Verify

```bash
# Discover and execute the project test runner invocation covering documentation loaders
# Discover and execute the static analysis command from the root project configuration
```

**Accept when:**
- The documentation loader pipeline successfully parses MDX sources and produces valid string representations.
- All automated test suites and static analysis checks covering document extraction execute without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests modifying documentation parsing or loader pipelines must pass automated continuous integration checks executing loader test suites and static analysis.
</enforcement>