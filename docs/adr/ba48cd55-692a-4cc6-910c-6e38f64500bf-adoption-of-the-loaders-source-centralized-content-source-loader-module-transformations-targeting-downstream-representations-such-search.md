# Adoption of the @/loaders/source Centralized Content Source Loader Module: Transformations Targeting Downstream Representations Such Search

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Multiple application routes including documentation displays, blog indexes, article details, search query handlers, and text extraction endpoints require synchronized access to content collections and page hierarchies.
- Decentralized loading of content sources introduces schema divergence, duplicated parsing overhead, and fragmented page tree representations across distinct presentation and utility boundaries.
- The project established a centralized internal source loader module to encapsulate content collection ingestion, search indexing contracts, and structural metadata resolution into a unified access point.

## Problem Statement

Without a unified content loading abstraction, documentation pages, blog views, search indexers, and plain text route handlers independently configure source ingestion pipelines, resulting in inconsistent content schemas, divergent route trees, and redundant parsing overhead.

## Decision

1. SHOULD: Transformations targeting downstream representations such as search indices or structured text outputs SHOULD derive their base collections directly from the centralized source loader module to maintain parity with rendered pages.

## Policy Block

- SHOULD Transformations targeting downstream representations such as search indices or structured text outputs SHOULD derive their base collections directly from the centralized source loader module to maintain parity with rendered pages.

In scope:
- All documentation pages, blog views, layout wrappers, search API handlers, and text generation utilities consuming content collections.
- Any new route or endpoint requiring access to structured content, navigation trees, or content metadata.

Out of scope:
- Static presentation components that receive pre-resolved content props without directly initiating content queries.
- Third-party asset serving and standalone endpoints independent of the content collection schema.

Exceptions:
- EXC-20-001: A specialized build script requires low-level content preprocessing prior to source loader initialization

## Rationale

- Evidence across seven files demonstrates consistent centralization where documentation layouts, dynamic route handlers, blog pages, search routes, and export pipelines all import the internal source loader module.
- Centralizing source extraction ensures that page routing, navigation sidebar hierarchies, search indices, and text generation share an identical content snapshot and validation ruleset.
- Isolating source configuration inside a dedicated module shields consumer components from breaking changes in underlying content transformation dependencies.

## Consequences

Positive:
- Guarantees schema consistency and navigation tree parity across documentation views, blog posts, search APIs, and export endpoints.
- Reduces duplicated content parsing and simplifies maintenance by providing a single point of configuration for content resolution.
- Decouples presentation components and route handlers from underlying content parsing and search indexing mechanics.

Negative:
- Introduces a centralized dependency where errors in the source loader module can cascade to all content-dependent routes.
- Limits route handlers from applying isolated, non-standard source parsing mechanisms without extending the shared module interface.

## Alternatives

- Decentralized direct filesystem and content parsing in each route handler (rejected)
  Rejected because: Creates duplicate parsing logic, increases memory footprint, and leads to divergent navigation hierarchies between documentation and search routes.
  When valid: Valid in simple applications with isolated single-page content rendering where centralized metadata is unnecessary.
- Third-party headless CMS client integration across routes (rejected)
  Rejected because: Introduces external network latency and operational complexity when content is already co-located within the repository workspace.
  When valid: Valid when content authorship is fully externalized to non-technical contributors via cloud CMS platforms.

## Risks

- Performance bottlenecks or memory amplification if the centralized source loader re-indexes content on un-cached requests.
  Mitigation: Ensure content collections and page tree caches are initialized once at build time or cached in memory across request lifecycles.
  Owner: engineering team
- Breaking API contract changes within underlying source libraries affecting the centralized loader module.
  Mitigation: Enforce strict dependency lockfile grounding and comprehensive integration tests covering all exported loader queries.
  Owner: engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Structure the centralized source loader module to export distinct query accessors for documentation trees, blog collections, and search records to avoid unnecessary full-source traversal.
- Ensure that search route handlers and text extraction utilities reuse existing parsed source entities rather than initiating independent file discovery cycles.

## Continuation Context


Verify commands:
- Discover and run the project type-checking script defined in the root configuration to verify all consumers adhere to the source loader interface.
- Discover and run the repository test suite to confirm source resolution, page tree generation, and search indexing pass without regression.
- Discover and execute the repository static analysis and linting scripts to verify compliance with the source loader import boundary.

Accept when:
- The project type-checking and static analysis scripts pass with zero errors across all content-consuming routes.
- All documentation, blog, search, and text export routes successfully resolve content through the centralized source loader module.

## Enforcement

- Verified by: Automated continuous integration checks executing repository linting, type validation, and test suites on pull requests.
- Verified by: Peer code review verifying that content queries are imported strictly from the centralized source loader module.
- Violation handling: Pull requests containing direct filesystem content loading or unapproved source loader instances are blocked until refactored to use the centralized module.
- Exception process: Submit an architectural review request outlining the specialized content ingestion requirements and obtain written approval from the lead architect.