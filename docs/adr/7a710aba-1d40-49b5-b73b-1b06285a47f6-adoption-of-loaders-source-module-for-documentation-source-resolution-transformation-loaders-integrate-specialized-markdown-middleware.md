---
version: 2
name: 7a710aba-1d40-49b5-b73b-1b06285a47f6-adoption-of-loaders-source-module-for-documentation-source-resolution-transformation-loaders-integrate-specialized-markdown-middleware
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

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `app/llms-full.txt/**`
- `loaders/**`

## Context

- The documentation subsystem serves multiple presentation and syndication targets, including structured web routes and aggregated full-text representations for automated consumers.
- Content source extraction requires consistent access to documentation page hierarchies, metadata parsing, and sequential document order across varied delivery endpoints.
- Dispersed and direct reading of content source files risks divergent parsing behavior, inconsistent frontmatter resolution, and fragmented navigation logic across consumers.
- The codebase establishes a centralized internal loader module to standardize content collection querying, page ordering, and transformation pipeline integration.

## Problem Statement

Without a unified content resolution mechanism, disparate documentation routes and transformation loaders independently parse source documents, leading to inconsistent metadata extraction, fragmented page ordering, and high maintenance overhead when documentation schemas evolve.

## Decision

1. MAY: Transformation loaders MAY integrate specialized markdown middleware to augment raw page content prior to serving serialized documentation representations.

## Policy Block

- MAY Transformation loaders MAY integrate specialized markdown middleware to augment raw page content prior to serving serialized documentation representations.

In scope:
- Documentation route handlers that expose structured or aggregated documentation content.
- Documentation loader utilities and transformation pipelines that query or compile documentation pages.

Out of scope:
- Static assets and media files stored outside the documentation page collection.
- Application components that do not interface with documentation source pages or frontmatter.

## Rationale

- Centralizing content retrieval behind @/loaders/source guarantees consistent page hierarchy resolution, frontmatter parsing, and navigation indexing across all consumer endpoints.
- Encapsulating third-party source loaders within an internal module isolates documentation routes from breaking changes in underlying source loading dependencies.
- Standardized loader interfaces enable specialized transformation utilities to process markdown content reliably without duplicating content discovery logic.

## Consequences

Positive:
- Enforces a single source of truth for documentation page structures and metadata extraction across endpoints.
- Simplifies endpoint logic by providing pre-structured page collections and ordering accessors.
- Shields application routes from direct dependencies on underlying content resolution libraries.

Negative:
- Couples content consumers to the specific data schema and interface exposed by the source loader module.
- Introduces memory overhead when maintaining page collections and order indices in runtime memory.

## Alternatives

- Direct filesystem traversal and markdown parsing in individual route handlers (rejected)
  Rejected because: Results in duplicated parsing logic, inconsistent metadata extraction, and maintenance hazards when frontmatter or file organization changes.
  When valid: Valid only in standalone single-page scripts with no shared navigation or indexing requirements.
- Direct unencapsulated consumption of third-party source libraries across all documentation routes (rejected)
  Rejected because: Exposes every route to breaking API changes from external dependencies and prevents centralized page ordering and transformation logic.
  When valid: Valid when building minimal documentation sites with no customized transformation pipelines or auxiliary endpoints.

## Risks

- Performance degradation if the source loader re-indexes content collections synchronously on repeated endpoint invocations.
  Mitigation: Derive and cache page lookup indices and navigation order during application initialization or build time.
  Owner: Engineering Team
- Interface drift between source loader exports and downstream transformation pipeline expectations.
  Mitigation: Define explicit type contracts for page objects and validate loader output through automated verification suites.
  Owner: Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Configure transformation pipelines by chaining dedicated markdown processing middleware sequentially to sanitize and format content extracted from the loader.
- Maintain sequential page order mappings in memory structures to facilitate rapid lookups when resolving predecessor and successor documentation routes.

## Continuation Context


Verify commands:
- Inspect the workspace configuration to discover the project verification script, then run the test suite to validate documentation loader resolution.
- Discover and run the project typecheck and linting commands from the package manifest to verify import boundary compliance across documentation endpoints.

Accept when:
- Documentation route handlers and text extraction loaders resolve page sources through @/loaders/source without import boundary errors.
- Automated verification suites confirm consistent page order indexing and successful content extraction across all endpoints.

## Enforcement

- Verified by: Static analysis checks configured in the continuous integration pipeline that flag unauthorized filesystem access in documentation routes.
- Verified by: Peer code review verifying that all documentation endpoints consume content via the canonical source loader.
- Violation handling: Pull requests containing direct filesystem access or bypasses of the source loader are rejected until refactored to use @/loaders/source.
- Violation handling: Architectural boundary alerts are triggered during automated build checks upon detection of unauthorized content parsing modules.
- Exception process: Exceptions must be submitted via an architecture review proposal detailing technical rationale, bounded scope, and fallback mechanisms.
- Exception process: Approval from lead documentation architects is required prior to merging any custom content loader.