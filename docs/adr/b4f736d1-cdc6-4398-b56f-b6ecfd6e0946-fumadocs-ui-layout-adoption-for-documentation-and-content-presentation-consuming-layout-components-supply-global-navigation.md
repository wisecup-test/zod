# fumadocs-ui Layout Adoption for Documentation and Content Presentation: Consuming Layout Components Supply Global Navigation

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Content and documentation routes require distinct structural presentations, distinguishing landing or blog pages from structured reference documentation layouts.
- Maintaining bespoke documentation layout trees introduces significant recurring maintenance cost for navigation bars, responsive sidebars, and hierarchical table of contents components.
- Static analysis reveals adoption of fumadocs-ui layout packages across route layout modules, backed by shared layout configuration modules.

## Problem Statement

Providing consistent, accessible, and responsive navigation across distinct documentation and content sections requires substantial structural UI boilerplate, leading to divergent layouts and duplicated layout logic if implemented independently per route.

## Decision

1. MUST: Consuming layout components MUST supply global navigation attributes through centralized shared layout configuration modules to maintain cross-route visual consistency.

## Policy Block

- MUST Consuming layout components MUST supply global navigation attributes through centralized shared layout configuration modules to maintain cross-route visual consistency.

In scope:
- Route layout components serving documentation, blog, or content landing pages within the documentation application.
- Shared configuration modules defining application-wide navigation, branding, and layout properties.

Out of scope:
- Standalone API routes, utility modules, and non-visual content processing scripts.
- Custom standalone web applications or embedded widgets that do not present documentation or publication content.

## Rationale

- Static evidence confirms the consistent adoption of fumadocs-ui layout modules across multiple route layout boundaries within the documentation application.
- Separating marketing or blog presentation from structured documentation through dedicated layout primitives keeps route boundaries focused and declarative.
- Leveraging third-party documentation layout primitives allows engineering focus to remain on content authoring and domain logic rather than custom navigation chrome maintenance.

## Consequences

Positive:
- Establishes standard structural boundaries separating content-focused blog presentations from hierarchical reference documentation layouts.
- Eliminates boilerplate navigation, sidebar tree traversal, and responsive chrome logic from internal application code.
- Centralizes shared layout configuration options through common configuration modules, ensuring uniform branding and navigation behavior.

Negative:
- Direct dependency on fumadocs-ui layout primitives introduces architectural coupling to third-party layout API design and upstream release lifecycles.
- Customization beyond the exported configuration interfaces of fumadocs-ui layout components requires composition overrides or library-level workarounds.
- Changes to upstream layout contract props require synchronized updates across all consuming route layout components.

## Alternatives

- Bespoke Custom Documentation and Blog Layout Implementation (rejected)
  Rejected because: Developing custom layout scaffolding increases maintenance burden, requires custom state tracking for navigation trees, and duplicates accessibility handling across routes.
  When valid: Valid when documentation presentation requirements strictly conflict with the layout primitives provided by specialized documentation libraries.
- Single Unified Layout Without Route-Specific Layout Modules (rejected)
  Rejected because: Coupling home, blog, and reference documentation structures into a single monolithic layout component produces brittle conditional rendering and inflates view complexity.
  When valid: Valid when the application consists solely of uniform reference pages with identical structural navigation needs.

## Risks

- Breaking changes in fumadocs-ui layout props or layout export structures during library version updates.
  Mitigation: Pin dependencies strictly using repository lock mechanisms and evaluate changelogs prior to layout library upgrades.
  Owner: engineering team
- Inconsistent navigation options between blog layouts and documentation layouts due to disparate configuration.
  Mitigation: Encapsulate global navigation options inside shared internal configuration modules to insulate layout routes from direct schema changes.
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
- Derive shared navigation, title, and theme parameters through a unified application layout configuration module to maintain consistency across distinct route layouts.
- Pass documentation tree sources and navigation loaders to specialized reference documentation layouts while keeping marketing and blog layouts decoupled from documentation source trees.

## Continuation Context


Verify commands:
- Discover and execute the repository type-checking script to verify interface compatibility between route layout boundaries and fumadocs-ui layout exports.
- Discover and execute the repository static analysis suite to verify absence of disallowed custom layout wrappers on documentation routes.
- Discover and execute the repository build script to confirm successful compilation of all route layout boundaries.

Accept when:
- Documentation route layouts successfully render navigation, sidebars, and body content using fumadocs-ui layout components without layout structural errors.
- All layout components resolve their configuration and source definitions through the standardized shared application configuration contract.
- The repository static verification suite passes without module resolution or layout contract violations.

## Enforcement

- Verified by: Automated static analysis and lint rules verifying that route layout boundaries import designated fumadocs-ui layout modules.
- Verified by: Continuous integration type-checking and automated build verification verifying layout property contracts against resolved library definitions.
- Verified by: Peer review verification during pull requests touching route layout boundaries.
- Violation handling: Pull request checks fail when route layout boundaries implement redundant custom navigation chrome instead of fumadocs-ui layout components.
- Violation handling: Violations must be remediated by refactoring layout boundaries to consume the standardized fumadocs-ui layout primitives and shared configuration.
- Exception process: Submit an architectural change proposal detailing why fumadocs-ui layout primitives cannot satisfy the presentation or navigation requirements of the specific route.
- Exception process: Review exceptions with the architecture review group and document any custom layout integration alongside the route boundary.