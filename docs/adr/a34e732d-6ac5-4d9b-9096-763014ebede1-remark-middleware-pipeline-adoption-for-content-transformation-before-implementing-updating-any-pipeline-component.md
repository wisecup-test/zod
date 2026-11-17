---
version: 2
name: a34e732d-6ac5-4d9b-9096-763014ebede1-remark-middleware-pipeline-adoption-for-content-transformation-before-implementing-updating-any-pipeline-component
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

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `loaders/**`

## Context

- The documentation loader architecture requires extraction and normalization of text content from MDX and Markdown sources for downstream consumption.
- Content sources incorporate varied syntax extensions including MDX components, file transclusion directives, and GitHub-flavored markdown formatting.
- Unifying document processing into an abstract syntax tree pipeline prevents fragmentation and avoids brittle regular expression substitutions across loaders.

## Problem Statement

Documentation text extraction and context generation require parsing Markdown and MDX documents that contain embedded syntax, file inclusions, and tables. Ad-hoc string manipulation or uncoordinated transformations fail to correctly handle complex abstract syntax trees, nested includes, and markdown flavors, leading to parsing inconsistencies across content loaders.

## Decision

1. MUST: Before implementing or updating any pipeline component, the consumer MUST inspect the repository lock artifact to determine the exact resolved versions of remark and all registered plugins.

## Policy Block

- MUST Before implementing or updating any pipeline component, the consumer MUST inspect the repository lock artifact to determine the exact resolved versions of remark and all registered plugins.

In scope:
- Documentation loader modules transforming Markdown and MDX content
- Text extraction pipelines preparing documentation content for downstream ingestion

Out of scope:
- Standard web application UI rendering pathways relying on native framework MDX compilation
- Plain text processing that does not parse or manipulate Markdown abstract syntax trees

## Rationale

- Chaining remarkMdx, remarkInclude, remarkGfm, and remarkStringify establishes an explicit, predictable pipeline order for AST mutations and output formatting.
- Using an established AST-based processor prevents parsing bugs and security vulnerabilities inherent in regex-based document preprocessing.
- The unified plugin architecture allows clean extension with additional syntax handlers without rewriting existing parsing logic.

## Consequences

Positive:
- Standardizes document transformation through an explicit, sequential middleware pipeline execution order.
- Enables modular additions or replacements of individual syntax transforms without altering loader infrastructure.
- Eliminates parsing regressions by processing content through formal syntax tree transformations rather than raw string heuristics.

Negative:
- Introduces dependency coordination overhead across multiple plugin packages that must maintain mutual compatibility.
- Increases memory and CPU consumption during document parsing compared to basic text streaming.

## Alternatives

- Regex-based text extraction and include resolution (rejected)
  Rejected because: Regular expressions fail on nested markdown structures, multi-line code blocks, and complex MDX tags, resulting in silent extraction errors.
  When valid: Valid only for trivial single-line string sanitization without structural markdown semantics.
- Full MDX compiler bundle evaluation at runtime (rejected)
  Rejected because: Evaluating full component bundles introduces unnecessary runtime overhead and security risks when only raw text extraction is required.
  When valid: Valid when rendering live interactive components in user interfaces.

## Risks

- Mismatches between unified plugin ecosystem releases causing runtime pipeline initialization failures
  Mitigation: Verify exact resolved lockfile versions for the unified processor and all registered plugins prior to deployment
  Owner: Documentation Infrastructure Team
- Circular file transclusion during recursive include resolution via remarkInclude
  Mitigation: Implement recursion depth bounds and cycle detection in document include configurations
  Owner: Documentation Infrastructure Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Assemble the remark pipeline builder once or configure a reusable loader helper rather than reinstantiating processor chains inside tight iteration loops.
- Ensure plugins that modify the abstract syntax tree structure precede remarkStringify to prevent unparsed syntax leaking into the generated output.

## Continuation Context


Verify commands:
- Discover the project test runner invocation from the dependency manifest and execute the test suite covering documentation loaders.
- Discover the static analysis command from the root project configuration and verify all loader pipeline definitions satisfy type and lint rules.

Accept when:
- The documentation loader pipeline successfully parses MDX sources and produces valid string representations.
- All automated test suites and static analysis checks covering document extraction execute without failure.

## Enforcement

- Verified by: Automated continuous integration checks executing loader test suites and static analysis.
- Verified by: Peer code review on all pull requests modifying documentation parsing or loader pipelines.
- Violation handling: Pull requests attempting manual string manipulation or unverified middleware pipeline configurations will be rejected during review.
- Exception process: Submit an architectural review request outlining why a specific document transform cannot be accommodated within the remark unified pipeline.