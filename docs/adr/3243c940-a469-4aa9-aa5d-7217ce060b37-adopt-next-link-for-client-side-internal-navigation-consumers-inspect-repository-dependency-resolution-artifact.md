# Adopt next/link for Client-Side Internal Navigation: Consumers Inspect Repository Dependency Resolution Artifact

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Documentation layouts, blog feeds, and interactive heading components require consistent intra-application navigation.
- Unmanaged hyperlink elements cause full page reloads, discarding application state and triggering unnecessary network overhead.
- The codebase requires a standardized routing primitive across both server-rendered and client-rendered components to support seamless page transitions.

## Problem Statement

Navigating between documentation articles, blog posts, and section anchors requires fast, smooth transitions without triggering full page reloads. Relying on unmanaged native hyperlink elements resets client-side state, causes content flashing, and fails to utilize prefetching capabilities provided by the application framework.

## Decision

1. MUST: Consumers MUST inspect the repository dependency resolution artifact to determine the exact locked version of the routing dependency before implementing navigation features.

## Policy Block

- MUST Consumers MUST inspect the repository dependency resolution artifact to determine the exact locked version of the routing dependency before implementing navigation features.

In scope:
- All internal navigation elements and section anchors within documentation and content routes.
- Interactive UI components that navigate between application views or routes.

Out of scope:
- Outbound links pointing to external domains or third-party web services.
- Static asset downloads requiring direct protocol handling.

Exceptions:
- EXC-20-001: Navigating to external domains or non-application protocols.

## Rationale

- Evidence across content pages and heading components establishes next/link as the uniform mechanism for handling local document traversal.
- Client-side routing preserves application execution context and optimizes user experience by prefetching destination routes.
- Centralizing internal navigation under a single framework primitive prevents mixed navigation patterns and redundant page loads.

## Consequences

Positive:
- Eliminates full page reloads during intra-application traversal, significantly improving navigation responsiveness.
- Enables automatic route prefetching for visible links within the viewport.
- Standardizes navigation link implementation across both server and client components.

Negative:
- Couples internal link rendering to the specific framework navigation module.
- Requires explicit handling for links that target external domains or alternate protocols.

## Alternatives

- Native HTML unmanaged anchor elements (rejected)
  Rejected because: Native unmanaged anchors trigger full page refreshes, discarding application state and degrading user experience.
  When valid: Valid only for links pointing to external web domains or downloadable file assets.
- Programmatic imperative routing via navigation hooks (rejected)
  Rejected because: Imperative routing degrades accessibility and search engine indexing compared to declarative link components.
  When valid: Valid only when navigation must occur as a side effect of asynchronous operational logic.

## Risks

- Accidental use of internal Link component for external URLs leading to unexpected routing errors.
  Mitigation: Establish linting and validation rules to detect external link schemas passed to internal navigation primitives.
  Owner: Frontend Engineering Team
- Excessive background prefetching causing redundant network data transfers.
  Mitigation: Configure viewport prefetching settings appropriately on pages with dense link indexes.
  Owner: Frontend Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- When wrapping custom typography or complex layout blocks with navigation capabilities, pass destination routes directly to the Link component to maintain standard document structure.
- Verify that external links or protocol-relative uniform resource identifiers bypass the framework navigation component and use standard outbound hyperlink elements with appropriate security attributes.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting scripts to verify compliance with internal link import rules.
- Discover and execute automated test suites to validate route link rendering and target attributes.
- Discover and run the project build script to ensure all linked routes resolve successfully.

Accept when:
- All internal intra-site links render via the framework Link component without unmanaged anchor tags for local paths.
- Project static analysis and build verification scripts execute without navigation-related errors.

## Enforcement

- Verified by: Automated static analysis checks in the continuous integration pipeline.
- Verified by: Peer code review for pull requests modifying navigational UI components or page routes.
- Violation handling: Pull requests containing unmanaged anchors for internal routes will be blocked until updated to use the designated routing module.
- Violation handling: Automated lint failures will halt continuous integration workflows.
- Exception process: Submit an architectural review request outlining why standard client routing cannot accommodate the specific navigational requirement.