# fumadocs-core Documentation Source Loading Architecture: Before Integrating Modifying Source Loader Modules

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Documentation subsystems require consistent loading, metadata indexing, and structural navigation across documentation source files.
- Multiple loader modules within the documentation package depend on fumadocs-core/source to construct source trees and feed downstream text processing and presentation pipelines.
- Decentralized file-system crawling and custom metadata extraction create divergent schemas and redundant parsing logic across documentation features.

## Problem Statement

Without a unified documentation source abstraction, modules responsible for rendering documentation pages and extracting documentation text implement fragmented file parsing and metadata inspection routines. This fragmentation risks structural divergence, inconsistent content indexing, and duplicated serialization logic across documentation features.

## Decision

1. MUST: Before integrating or modifying source loader modules, the consumer MUST discover the project dependency manifest and authoritative lock artifact to inspect and confirm the exact resolved version of fumadocs-core and its companion packages.

## Policy Block

- MUST Before integrating or modifying source loader modules, the consumer MUST discover the project dependency manifest and authoritative lock artifact to inspect and confirm the exact resolved version of fumadocs-core and its companion packages.

In scope:
- Documentation loader definitions and content tree resolution routines
- Pipelines extracting or transforming documentation content from managed collections

Out of scope:
- Application domain data management outside documentation boundaries
- Static assets and unmanaged raw assets not indexed as documentation sources

## Rationale

- Adopting fumadocs-core/source establishes a single, structured interface for navigating documentation trees and resolving page metadata across multiple consuming utilities.
- Code evidence demonstrates that both document loading and specialized text extraction pipelines rely on fumadocs-core/source to maintain schema consistency and unified collection traversal.
- Centralizing content access within the adopted library boundary minimizes maintenance overhead compared to developing and maintaining bespoke document-crawling infrastructure.

## Consequences

Positive:
- Provides a standardized content structure and typed navigation API across all documentation consumers.
- Eliminates duplicate directory scanning, frontmatter parsing, and hierarchy reconstruction logic across utilities.
- Ensures structural alignment between documentation presentation components and auxiliary content extraction workflows.

Negative:
- Introduces architectural coupling to fumadocs-core source schemas and collection lifecycle expectations.
- Upgrading the documentation framework requires verifying source API compatibility across all custom loader extensions.

## Alternatives

- Custom file-system crawler with manual frontmatter parsing and tree assembly (rejected)
  Rejected because: Increases maintenance burden and introduces risk of schema divergence between documentation presentation and auxiliary utilities.
  When valid: When building documentation systems in runtime environments where fumadocs dependencies cannot be executed.
- Decentralized loader definitions implemented independently within each consuming module (rejected)
  Rejected because: Duplicates source configuration and increases the likelihood of inconsistent page metadata resolution across consumers.
  When valid: When consumers require fundamentally incompatible representations of source documents that cannot share a schema.

## Risks

- Breaking API changes across library version upgrades could disrupt dependent loader pipelines.
  Mitigation: Strict adherence to lock-version grounding and automated type checking during dependency upgrades.
  Owner: engineering team
- Coupling specialized extraction workflows to source structures might limit markdown preprocessing flexibility.
  Mitigation: Encapsulate specialized AST transformations within modular loader pipelines while preserving the core source abstraction.
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
- Define a primary source loader module that initializes collection schemas and exports unified page accessors.
- Ensure transformation pipelines reuse the exported source tree rather than reconstructing source hierarchies independently.

## Continuation Context


Verify commands:
- Discover the project verification script declared in the dependency manifest and run type checking across documentation modules.
- Discover and execute the project test suite to verify that documentation source loaders successfully resolve collections and page metadata.

Accept when:
- Type verification completes with zero diagnostics across all source loader and content consumer modules.
- Test executions confirm valid collection traversal and consistent metadata extraction from the centralized source loader.

## Enforcement

- Verified by: Automated type verification in continuous integration workflows.
- Verified by: Peer review verifying that documentation content access routes through the standardized source loader.
- Violation handling: Pull requests introducing direct file reads or ad-hoc markdown parsing for documentation pages must be blocked.
- Violation handling: Offending implementations must be refactored to consume the centralized source loader interface.
- Exception process: Exceptions require architectural review documenting why the centralized source loader cannot support the specific content format.
- Exception process: Approved exceptions must document isolation boundaries and schema translation mechanisms.