---
version: 2
name: 311b950c-1e80-4452-bd6d-33bece33dc9a-react-mutable-ref-map-pattern-for-dom-node-caching-components-not-store-mutable-dom-element
description: "React Mutable Ref Map Pattern for DOM Node Caching: Components Not Store Mutable Dom Element"
metadata:
  actual:
    adr_id: 311b950c-1e80-4452-bd6d-33bece33dc9a
    status: accepted
    candidate_group_id: 3b215305-688a-477b-83d0-704f562c9c03
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Mutable Ref Map Pattern for DOM Node Caching: Components Not Store Mutable Dom Element

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `components/**`

## Context

- Interactive client navigation components require continuous tracking of active heading positions during viewport scrolling to calculate indicator dimensions and offsets.
- Repeatedly querying the global document object model for element identifiers incurs DOM access overhead and potential layout thrashing during high-frequency scroll and resize events.
- Storing DOM node references in standard component state would trigger component re-render cascades whenever element maps update, degrading scrolling performance.
- The component utilizes a React mutable reference wrapping a key-value Map to cache DOM element nodes locally across render lifecycles.

## Problem Statement

Client-rendered navigation components that dynamically position active indicators need access to target DOM nodes without triggering reactive re-render cycles or incurring overhead from repetitive document tree queries. Without an in-memory caching strategy for element references, scroll position handlers must repeatedly scan the DOM or synchronize layout changes through state updates that degrade rendering performance.

## Decision

1. MUST_NOT: Components MUST_NOT store mutable DOM element references in reactive component state when the updates do not alter the rendered markup hierarchy.

## Policy Block

- MUST_NOT Components MUST_NOT store mutable DOM element references in reactive component state when the updates do not alter the rendered markup hierarchy.

In scope:
- Client-rendered navigation components that measure and track DOM element positions dynamically.
- Components maintaining active indicators synchronized with scroll or focus events.

Out of scope:
- Server-rendered components that do not execute in client browser environments.
- Components where element collections are static and do not require runtime coordinate calculations.

## Rationale

- Using a React mutable ref holding a key-value Map maintains direct element references without triggering unwanted re-render cycles upon mutation.
- In-memory caching avoids repetitive document queries during rapid scroll events, minimizing layout calculation latency.
- Encapsulating cache access within lifecycle hooks and memoized callbacks maintains deterministic registration and cleanup of DOM nodes.

## Consequences

Positive:
- Decouples layout tracking from reactive state, eliminating unnecessary component re-renders during high-frequency scroll events.
- Provides constant-time lookup for target DOM nodes during indicator position calculations.
- Isolates DOM reference mutations within the component lifecycle boundary.

Negative:
- Requires explicit manual lifecycle management to add and delete elements, increasing the risk of memory leaks if cleanup is omitted.
- Circumvents standard reactive data flow by storing mutable instance references outside component state.
- Limits pattern utility to client-rendered environments where the document object model is accessible.

## Alternatives

- Reactive state storage for element references using useState (rejected)
  Rejected because: Updating state on element mounting and position tracking triggers component re-renders that induce layout recalculation and frame drops during scrolling.
  When valid: Valid when child components or markup structures must reactively re-render in direct response to element collection changes.
- Global document query lookups on demand (rejected)
  Rejected because: Executing document element queries repeatedly inside scroll event listeners adds query parsing overhead and potential layout thrashing.
  When valid: Valid when element counts are negligible and lookups occur infrequently outside high-frequency event loops.

## Risks

- Failure to delete unmounted elements from the Map creates memory leaks by retaining detached DOM nodes in memory.
  Mitigation: Ensure ref callbacks or hook cleanup routines explicitly invoke delete on the Map instance when elements unmount.
  Owner: Frontend Engineering Team
- Accessing cached ref nodes before mounting or after DOM mutations may return stale or null element coordinates.
  Mitigation: Verify element existence and null safety checks on every cache retrieval before reading layout properties.
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
- Initialize the mutable reference with a new Map instance and manage element associations using a ref callback function attached to rendered items.
- Execute measurement logic within an effect hook or resize observer to read bounding rects from cached elements only when the active target changes.

## Continuation Context


Verify commands:
- Discover and execute the project test runner to validate component rendering and active element indicator calculations.
- Discover and execute the static type checker to ensure proper typing of ref collections and element map accessors.
- Discover and execute the project linter to enforce hook dependency rules and prevent improper ref modifications during render.

Accept when:
- Component tests pass with all target DOM nodes correctly registered, accessed, and cleaned up upon unmount.
- Type checking completes with zero errors across mutable ref definitions and Map operations.
- Lint analysis reports no violations for hook dependency arrays or mutable ref assignments during render.

## Enforcement

- Verified by: Automated pull request continuous integration checks verifying test suites, linting rules, and type compliance.
- Verified by: Peer code review validating correct cleanup logic and preventing reactive state misuse for DOM caching.
- Violation handling: Pull requests introducing state-based DOM element tracking or missing cache cleanup handlers must be rejected.
- Violation handling: Violations identified during code review require refactoring to use the mutable ref Map pattern before merge.
- Exception process: Submit an architectural review request demonstrating that reactive state synchronization is strictly required for the component layout.
- Exception process: Obtain written approval from the frontend architecture lead prior to merging alternative DOM tracking implementations.