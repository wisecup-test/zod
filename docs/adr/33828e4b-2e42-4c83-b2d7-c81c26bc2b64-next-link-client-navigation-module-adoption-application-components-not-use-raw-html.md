---
version: 2
name: 33828e4b-2e42-4c83-b2d7-c81c26bc2b64-next-link-client-navigation-module-adoption-application-components-not-use-raw-html
description: "next/link Client Navigation Module Adoption: Application Components Not Use Raw Html"
metadata:
  actual:
    adr_id: 33828e4b-2e42-4c83-b2d7-c81c26bc2b64
    status: accepted
    candidate_group_id: 8497fb63-f882-4406-98b2-b60281fa558a
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/blog/**
      - components/**
---

# next/link Client Navigation Module Adoption: Application Components Not Use Raw Html

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `app/blog/**`
- `components/**`

## Context

- Documentation components and page views require seamless internal hyperlinking to facilitate content navigation.
- Direct browser navigation using unmanaged anchor tags discards client runtime state and degrades page transition latency.
- Multiple user interface elements across the documentation package standardize on next/link to manage internal routing.

## Problem Statement

Navigating between internal documentation routes using standard unmanaged browser anchors triggers full document reloads, discarding client-side runtime state and increasing page transition latency.

## Decision

1. MUST_NOT: Application components MUST NOT use raw HTML anchor elements for internal route navigation when declarative client routing is available.

## Policy Block

- MUST_NOT Application components MUST NOT use raw HTML anchor elements for internal route navigation when declarative client routing is available.

In scope:
- All page views and interactive UI components requiring navigation between internal application routes.

Out of scope:
- External hyperlinks pointing to third-party domains or non-routed static file downloads.

## Rationale

- Standardizing on next/link enables seamless client-side page transitions while retaining application memory state.
- Automated route prefetching optimizes user navigation across documentation articles and index listings.
- Consistent component adoption prevents mixed routing paradigms across documentation pages and UI primitives.

## Consequences

Positive:
- Preserves in-memory client state across page transitions without triggering browser full-page reload cycles.
- Accelerates subsequent route navigation latency via automated background prefetching of linked route assets.
- Ensures consistent navigation semantics across all documentation components and layout templates.

Negative:
- Increases client JavaScript bundle footprint compared to unadorned native anchor elements.
- Introduces background network overhead when multiple links prefetch destination routes within the viewport.

## Alternatives

- Standard HTML anchor elements for internal navigation (rejected)
  Rejected because: Triggers full document reloading, resets application state, and bypasses client-side prefetching.
  When valid: Valid only for external hyperlinks or file downloads outside the application router.
- Programmatic imperative navigation hooks for all interactive links (rejected)
  Rejected because: Complicates declarative component templates and degrades search crawler accessibility.
  When valid: Valid when navigation is strictly conditional upon asynchronous operations or form validations.

## Risks

- Aggressive viewport prefetching could trigger superfluous network requests on bandwidth-constrained clients.
  Mitigation: Configure prefetch properties to avoid unnecessary data fetching for offscreen or dense link collections.
  Owner: engineering team
- Nested interactive elements inside link components could trigger hydration errors or invalid markup hierarchies.
  Mitigation: Enforce component linting and semantic markup validation during code review.
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
- Wrap next/link instances in presentation components when applying design system utility styling or responsive layout rules.
- Ensure passing appropriate accessibility attributes and destination href values to maintain keyboard navigability and semantic structure.

## Continuation Context


Verify commands:
- Discover and execute the repository static analysis and linting scripts to identify non-compliant anchor usage.
- Discover and execute the repository test runner to verify navigation component rendering and routing integrity.

Accept when:
- All internal navigation hyperlinks render through next/link without unmanaged anchor element fallbacks.
- Repository static analysis and test validation suites pass without routing rule violations.

## Enforcement

- Verified by: Static analysis and lint checks in continuous integration pipelines.
- Verified by: Code reviews of pull requests introducing or modifying routing components.
- Violation handling: Build failure when disallowed anchor tags are detected for internal routes.
- Violation handling: Review rejection during pull request evaluation.
- Exception process: Submit an architectural exception request documenting requirements for external routing or legacy anchor integration.
- Exception process: Obtain approval from architecture leads prior to merging.