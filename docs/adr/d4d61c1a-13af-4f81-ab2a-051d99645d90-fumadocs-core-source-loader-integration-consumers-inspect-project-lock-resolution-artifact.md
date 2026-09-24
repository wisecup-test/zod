# fumadocs-core Source Loader Integration: Consumers Inspect Project Lock Resolution Artifact

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Documentation workspaces require structured mechanisms to discover, organize, and traverse document hierarchies for web rendering and automated text generation.
- The documentation application maintains loader utilities and HTTP route handlers that generate complete textual representations of documentation pages.
- Adopting a standardized content source module centralizes document schema validation, page tree discovery, and metadata indexing in a single shared interface.
- Downstream route handlers and serialization utilities require structured access to document pages and ordering schemas to ensure deterministic content exports.

## Problem Statement

Documentation applications require reliable, structured access to page hierarchies, content trees, and page metadata for rendering and downstream text extraction. Without a unified content source loader abstraction, route handlers and loader utilities tend to implement divergent, ad-hoc filesystem reads and metadata parsing, leading to inconsistent page ordering, fragile path resolution, and duplicated AST transformation pipelines across endpoints.

## Decision

1. MUST: Consumers MUST inspect the project lock and resolution artifact to resolve the exact installed version of fumadocs-core before consuming or altering source loader interfaces, ensuring API compatibility with the active environment.

## Policy Block

- MUST Consumers MUST inspect the project lock and resolution artifact to resolve the exact installed version of fumadocs-core before consuming or altering source loader interfaces, ensuring API compatibility with the active environment.

In scope:
- Documentation workspace modules responsible for loading, indexing, or traversing page content.
- Route handlers and loader utilities that serialize documentation pages for downstream consumers.

Out of scope:
- Application components and UI layouts consuming pre-rendered page data.
- Non-documentation packages and external service endpoints within the repository.

## Rationale

- Adopting fumadocs-core/source establishes a consistent contract for document discovery, eliminating fragmented filesystem traversal logic across endpoints.
- Centralizing source loading decouples content representation from endpoint serialization, enabling specialized route handlers to transform page ASTs uniformly.
- Structured page tree access simplifies in-memory page ordering and indexing, ensuring reliable metadata resolution and deterministic text generation.

## Consequences

Positive:
- Single point of maintenance for content ingestion, page hierarchy traversal, and frontmatter metadata resolution.
- Guaranteed consistency between documentation web views and automated full-text export endpoints.
- Standardized AST transformation pipeline integration for formatting documentation across different consumer interfaces.

Negative:
- Direct coupling to the fumadocs-core source loader API contract across all documentation loader consumers.
- Source updates or breaking schema migrations in the core library require coordinated updates across internal loader wrappers and consuming routes.

## Alternatives

- Manual filesystem scanning with direct frontmatter and markdown parsing (rejected)
  Rejected because: Increases maintenance burden, duplicates path resolution and metadata parsing logic across routes, and fails to provide structured page tree hierarchies out of the box.
  When valid: Valid only in standalone single-page scripts with no hierarchical documentation structure.
- Custom bespoke content repository abstraction built entirely in-house (rejected)
  Rejected because: Reinvents existing framework source loading capabilities, requiring ongoing maintenance of custom tree traversal, page caching, and schema validation.
  When valid: Valid when content is hosted in a proprietary remote database with non-standard relational hierarchies.

## Risks

- Upstream updates to fumadocs-core/source could alter source loader method signatures or page tree representations.
  Mitigation: Encapsulate framework source calls behind internal loader module wrappers and verify resolved versions against the lock artifact prior to upgrades.
  Owner: Documentation Engineering
- In-memory caching of page ordering in route handlers could consume excessive memory if page count grows drastically.
  Mitigation: Bound cache scopes to request lifecycles and limit indexed properties to essential routing identifiers and order indices.
  Owner: Documentation Engineering

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Centralize source loader configuration in a shared loader module within the documentation workspace so downstream utilities and route handlers consume a uniform interface.
- Compose AST transformation middleware in dedicated loader helper functions to keep HTTP route handlers focused on request handling and serialization.

## Continuation Context


Verify commands:
- Discover the workspace root configuration to locate the documentation test execution task, then execute the suite to verify source loader compatibility.
- Identify the project type check script in the package manifest and run the type checker across documentation modules to validate source loader call signatures.
- Locate and execute the documentation build validation script to ensure route handlers correctly resolve and serialize pages via the source loader.

Accept when:
- All source loader consumers and route handlers compile without type errors against the resolved source module definitions.
- Documentation endpoints successfully traverse the page hierarchy and serialize page content through the centralized source loader interface.
- Test suites validating documentation content extraction and page ordering pass with zero regressions.

## Enforcement

- Verified by: Automated static analysis and type checking in the continuous integration pipeline.
- Verified by: Peer code reviews on all modifications to documentation loader interfaces and route handlers.
- Violation handling: Pull requests introducing direct filesystem parsing or bypassing the central source loader must be blocked until refactored to use the standardized source interface.
- Violation handling: Static analysis failures flagging unauthorized direct markdown reading must prevent merge.
- Exception process: Exceptions for auxiliary metadata files not managed by the source loader must be documented in code review and approved by the documentation architecture maintainers.