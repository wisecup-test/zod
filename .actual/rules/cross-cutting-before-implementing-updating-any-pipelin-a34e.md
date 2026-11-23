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

These rules are ALWAYS ACTIVE for:
- Documentation loader modules transforming Markdown and MDX content
- Text extraction pipelines preparing documentation content for downstream ingestion

### Rules

- **R-ISP-001** MUST: Before implementing or updating any pipeline component, the consumer MUST inspect the repository lock artifact to determine the exact resolved versions of remark and all registered plugins.

### Verify

- Discover the project test runner invocation from the dependency manifest and execute the test suite covering documentation loaders.
- Discover the static analysis command from the root project configuration and verify all loader pipeline definitions satisfy type and lint rules.

**Accept when:**

- The documentation loader pipeline successfully parses MDX sources and produces valid string representations.
- All automated test suites and static analysis checks covering document extraction execute without failure.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks executing loader test suites and static analysis.
- Verified by: Peer code review on all pull requests modifying documentation parsing or loader pipelines.
- Violation handling: Pull requests attempting manual string manipulation or unverified middleware pipeline configurations will be rejected during review.
- Exception process: Submit an architectural review request outlining why a specific document transform cannot be accommodated within the remark unified pipeline.
</enforcement>
