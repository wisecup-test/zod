---
version: 2
name: cross-cutting-transformation-loaders-integrate-special-7a71
description: "Adoption of @/loaders/source Module for Documentation Source Resolution: Transformation Loaders Integrate Specialized Markdown Middleware"
metadata:
  actual:
    adr_id: 7a710aba-1d40-49b5-b73b-1b06285a47f6
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

# Adoption of @/loaders/source Module for Documentation Source Resolution: Transformation Loaders Integrate Specialized Markdown Middleware

Scope: applies to `packages/docs/app/llms-full.txt/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for:
- Documentation route handlers that expose structured or aggregated documentation content.
- Documentation loader utilities and transformation pipelines that query or compile documentation pages.

### Rules

- **R-LM-001** MAY: Transformation loaders MAY integrate specialized markdown middleware to augment raw page content prior to serving serialized documentation representations.

### Verify

- Inspect the workspace configuration to discover the project verification script, then run the test suite to validate documentation loader resolution.
- Discover and run the project typecheck and linting commands from the package manifest to verify import boundary compliance across documentation endpoints.

**Accept when:**

- Documentation route handlers and text extraction loaders resolve page sources through @/loaders/source without import boundary errors.
- Automated verification suites confirm consistent page order indexing and successful content extraction across all endpoints.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Static analysis checks configured in the continuous integration pipeline that flag unauthorized filesystem access in documentation routes.
- Verified by: Peer code review verifying that all documentation endpoints consume content via the canonical source loader.
- Violation handling: Pull requests containing direct filesystem access or bypasses of the source loader are rejected until refactored to use @/loaders/source.
- Violation handling: Architectural boundary alerts are triggered during automated build checks upon detection of unauthorized content parsing modules.
- Exception process: Exceptions must be submitted via an architecture review proposal detailing technical rationale, bounded scope, and fallback mechanisms.
- Exception process: Approval from lead documentation architects is required prior to merging any custom content loader.
</enforcement>
