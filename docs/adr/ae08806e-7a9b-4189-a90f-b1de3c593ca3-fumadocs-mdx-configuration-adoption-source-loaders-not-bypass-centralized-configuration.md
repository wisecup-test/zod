# Fumadocs MDX Configuration Adoption: Source Loaders Not Bypass Centralized Configuration

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The documentation subsystem requires a standardized mechanism for defining content sources, schema configurations, and MDX processing pipelines.
- Documentation modules coordinate source loading and text transformation through structured configuration contracts rather than unconstrained file-system scripts.
- Static analysis identifies consistent integration of fumadocs-mdx/config across documentation source configuration and content extraction loaders.

## Problem Statement

Documentation content processing pipelines require consistent source schema validation, metadata extraction, and MDX compilation controls across documentation loaders. Without a centralized configuration module, documentation loaders risk divergent schema interpretations, ad-hoc Markdown parsing, and uncoordinated content definitions.

## Decision

1. MUST_NOT: Source loaders MUST NOT bypass the centralized configuration schema when extracting structured documentation content.

## Policy Block

- MUST_NOT Source loaders MUST NOT bypass the centralized configuration schema when extracting structured documentation content.

In scope:
- Documentation subsystem modules defining content sources, schema collections, or MDX processing loaders.
- Modules responsible for extracting and transforming structured documentation content.

Out of scope:
- Non-documentation workspace packages and runtime application modules.
- Standalone static assets that do not undergo MDX compilation or source schema extraction.

## Rationale

- Adopting a standardized configuration module unifies documentation schemas and content loaders around a shared configuration contract.
- Evidence demonstrates consistent dependency on fumadocs-mdx/config across configuration and extraction loaders, preventing configuration divergence.
- Decoupling content definition from rendering through a centralized configuration module enables downstream loaders to process MDX sources reliably.

## Consequences

Positive:
- Unified configuration contract across documentation content sources and loader utilities.
- Consistent MDX transformation pipeline behavior with reproducible source resolution.
- Reduced duplication in document parsing and metadata extraction logic.

Negative:
- Subsystem dependencies become tightly coupled to the configuration conventions of the adopted documentation framework.
- Changes to content collection schemas require synchronized updates across all dependent loader modules.

## Alternatives

- Custom ad-hoc file-system parsing and manual frontmatter extraction (rejected)
  Rejected because: Increases maintenance overhead and creates fragmented schema validation across documentation loader scripts.
  When valid: Lightweight documentation sites with minimal content files and no requirement for MDX compilation pipelines.
- Fumadocs MDX configuration module adoption (accepted)
  Rejected because: None
  When valid: Documentation workspaces requiring structured content collections, MDX processing pipelines, and consistent loader access.

## Risks

- Breaking API changes in upstream configuration releases could disrupt documentation content loading.
  Mitigation: Strictly adhere to the resolved lock-file version and validate configuration contracts during automated builds.
  Owner: Documentation Engineering Team
- Content loaders bypassing centralized configuration could introduce divergent document structures.
  Mitigation: Enforce architectural boundaries through automated linting and code review checks.
  Owner: Documentation Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Discover the workspace dependency manifest to locate documentation configuration entry points before adding new content collections.
- Ensure that custom markdown and remark transformation plugins integrate directly with the source loader processing chain.

## Continuation Context


Verify commands:
- Discover the workspace dependency manifest, locate the documentation validation script, and execute it using the project task runner.
- Locate the workspace typecheck script and run it to verify that all documentation source configurations and loaders conform to type definitions.

Accept when:
- Documentation source configurations compile without type errors.
- Content loader pipelines successfully parse and extract structured documentation text.

## Enforcement

- Verified by: Continuous integration automated typecheck and build validation pipelines.
- Verified by: Peer code review for pull requests modifying documentation loaders and source configurations.
- Violation handling: Build failures in automated continuous integration workflows.
- Violation handling: Rejection of pull requests that bypass the centralized configuration module.
- Exception process: Submit an architectural review request documenting the rationale for custom content loading mechanisms.