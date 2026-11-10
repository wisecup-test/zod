---
version: 2
name: 352a4d32-ca4c-4ac2-8b36-c58333a8a8b5-react-client-component-interaction-architecture-components-not-reference-browser-global-objects
description: "React Client Component Interaction Architecture: Components Not Reference Browser Global Objects"
metadata:
  actual:
    adr_id: 352a4d32-ca4c-4ac2-8b36-c58333a8a8b5
    status: accepted
    candidate_group_id: f9a2d8cc-8daa-42ab-90ec-25b61d21e072
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Client Component Interaction Architecture: Components Not Reference Browser Global Objects

Status: proposed
Date: 2025-02-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `components/**`

## Context

- Frontend documentation components require dynamic capabilities including active heading tracking, clipboard interaction, dynamic logo loading, and external search modal mounting.
- Server-side rendering constraints prohibit direct access to browser window APIs, DOM measurements, and interactive event handlers without an explicit runtime boundary.
- Multiple components across the documentation interface implement client boundary directives alongside React state and effect hooks to manage localized interaction lifecycles.

## Problem Statement

UI components in the documentation layer need to execute browser-specific logic and manage interactive state without compromising server rendering guarantees or creating inconsistent lifecycle patterns across interactive controls.

## Decision

1. MUST_NOT: Components MUST NOT reference browser global objects or perform DOM mutations outside of client lifecycle hooks or client event handlers.

## Policy Block

- MUST_NOT Components MUST NOT reference browser global objects or perform DOM mutations outside of client lifecycle hooks or client event handlers.

In scope:
- All interactive UI components authoring client-side state, DOM manipulation, or third-party client integrations in frontend documentation packages.

Out of scope:
- Static server-rendered content components, pure layout shells without state, and headless utility modules.

## Rationale

- Static analysis of seven UI component modules demonstrates uniform adherence to React client boundaries and standard React interaction hooks.
- Enforcing explicit client component boundaries ensures clean isolation of client execution runtimes from server-rendered document structures.
- Standardizing on useState, useEffect, and useCallback guarantees predictable lifecycle handling, state encapsulation, and memory leak prevention across disparate controls.

## Consequences

Positive:
- Predictable lifecycle management and clear separation between server-rendered layouts and interactive client controls.
- Consistent handling of browser APIs, clipboard integrations, and third-party UI integrations across the documentation site.
- Prevention of memory leaks through structured effect cleanup patterns.

Negative:
- Increased client bundle payload for components marked with the client directive.
- Hydration overhead for components requiring client-side mounting and DOM reconciliation.
- Inability to directly leverage server-only capabilities within components marked as client boundaries.

## Alternatives

- Global client-side application state store for all component interactions (rejected)
  Rejected because: Introduces unnecessary architectural coupling and bundle weight for localized component interactions such as copy buttons and scroll trackers.
  When valid: When state must be synchronized across disparate layout hierarchies or persisted globally across routing transitions.
- Pure vanilla DOM manipulation outside React component lifecycle (rejected)
  Rejected because: Bypasses declarative React reconciliation, risking desynchronization between virtual DOM and actual DOM state.
  When valid: When integrating low-level canvas or web worker pipelines that operate independently of the component rendering tree.

## Risks

- Hydration mismatch if client components render state-dependent DOM before initial mount completes.
  Mitigation: Defer browser-specific conditional rendering until after mounting within useEffect or initialize with consistent server-safe fallback state.
  Owner: Frontend engineering team
- Memory leaks from uncleaned event listeners or interval timers inside useEffect hooks.
  Mitigation: Enforce explicit return of cleanup functions in all effect hooks establishing external subscriptions.
  Owner: Frontend engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Position client component boundaries at leaf nodes of the component hierarchy whenever possible to maximize server rendering coverage.
- Encapsulate third-party client integrations into dedicated wrapper components that manage initialization and teardown within localized effects.

## Continuation Context


Verify commands:
- Discover the workspace static analysis script from the project manifest and run it to verify compliance with hook usage and client directive requirements.
- Discover the project automated test script from the project manifest and execute it to validate interactive component behavior and state transitions.
- Discover the project type checking script from the project manifest and run it to verify type safety across component props and hook dependencies.

Accept when:
- All interactive UI components declare the client directive at the module root and pass static analysis without lint violations.
- All component interaction tests execute successfully with zero unhandled exceptions or effect lifecycle warnings.
- Static type checking completes with zero diagnostic errors across all client component files.

## Enforcement

- Verified by: Automated continuous integration pipeline executing static analysis and lint checks.
- Verified by: Peer code review verifying component boundary placement and effect cleanup logic.
- Violation handling: Pull requests containing unencapsulated browser API access or missing client directives are blocked by continuous integration checks.
- Violation handling: Identified violations must be refactored into compliant client component hooks before merging.
- Exception process: Submit an architectural variance request documented in the relevant pull request outlining why a non-standard interaction mechanism is required.
- Exception process: Obtain approval from the frontend architecture lead prior to merging.