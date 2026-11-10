---
version: 2
name: 0b0f5a30-c8f7-4d9b-8f3c-c45fd4d57d85-react-server-component-client-boundary-demarcation-via-use-client-directive-client-boundary-directives-placed-leaf-level
description: "React Server Component Client Boundary Demarcation via use client Directive: Client Boundary Directives Placed Leaf Level"
metadata:
  actual:
    adr_id: 0b0f5a30-c8f7-4d9b-8f3c-c45fd4d57d85
    status: accepted
    candidate_group_id: acff8b33-9c51-4920-90b0-98df262c0044
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Server Component Client Boundary Demarcation via use client Directive: Client Boundary Directives Placed Leaf Level

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `components/**`

## Context

- The application UI framework employs a server-first rendering model where components execute on the server by default.
- Certain UI components require client-side interactivity, DOM event handling, local component state, or browser-specific lifecycle execution.
- Third-party UI libraries for interactive widgets, accordions, and external integrations depend on browser APIs and client-side React contexts that are unavailable in server environments.
- A clear architectural boundary mechanism is required to explicitly designate which component modules execute in the client runtime without unnecessarily opting out parent or child trees from server rendering.

## Problem Statement

Within a server-first React component architecture, components default to server execution where browser APIs, DOM manipulation, and interactive React lifecycle hooks are inaccessible. Interactive elements such as search dialogs, table-of-contents trackers, collapsible accordions, and interactive buttons fail to execute without an explicit boundary declaration designating their modules for client-side evaluation and hydration.

## Decision

1. SHOULD: Client boundary directives SHOULD be placed at leaf-level interactive components to maximize server-rendered markup and minimize client bundle size.

## Policy Block

- SHOULD Client boundary directives SHOULD be placed at leaf-level interactive components to maximize server-rendered markup and minimize client bundle size.

In scope:
- All frontend UI components within the documentation and web interface packages requiring interactive state, DOM manipulation, or browser APIs.
- Integration wrapper components interfacing with client-only third-party UI widgets and search dialogs.

Out of scope:
- Purely static presentational components that render markup without client-side state, event handlers, or browser APIs.
- Server-side data fetching layouts, page entries, and static document transformation utilities.

## Rationale

- Explicit boundary demarcation with the use client directive allows interactive components to access browser APIs and lifecycle hooks while preserving server-rendering benefits for surrounding layouts.
- Applying the boundary directive at the component module level keeps client JavaScript bundles minimal by preventing unnecessary client-side bundling of static page content.
- Consistent use of the directive across fourteen distinct component modules demonstrates an established architectural pattern for integrating client interactivity with external UI libraries.

## Consequences

Positive:
- Enables full access to browser APIs, DOM node references, and interactive React lifecycle hooks within designated components.
- Maintains clear structural separation between server-rendered content and interactive client widgets.
- Allows seamless integration with client-dependent third-party UI primitive libraries and external interactive search widgets.

Negative:
- Increases client JavaScript bundle size and hydration overhead for every module opted into the client boundary.
- Requires careful boundary placement to avoid unintentionally converting static server-rendered child trees into client-rendered subtrees.
- Introduces architectural friction when sharing utility functions or types between server and client component boundaries.

## Alternatives

- Universal client-side rendering for the entire component tree (rejected)
  Rejected because: Forces all components and their dependencies into the client JavaScript bundle, eliminating server-side rendering performance gains, increasing initial page load latency, and inflating hydration overhead.
  When valid: Valid only in purely client-side single-page applications without server component runtime support.
- Deferring client boundaries exclusively to top-level layout pages (rejected)
  Rejected because: Cascades client execution to all child subtrees, preventing leaf-level server rendering and leaking client runtime dependencies across static presentation elements.
  When valid: Valid when every descendant element within a layout inherently depends on continuous client-side application state or context providers.

## Risks

- Overusing client boundaries on high-level components can inadvertently force large static subtrees into client bundles, increasing payload sizes and hydration times.
  Mitigation: Enforce linting and code review standards to keep client boundary declarations near leaf nodes rather than high-level layout containers.
  Owner: Frontend Engineering Team
- Third-party component packages may assume a client runtime environment, causing server build breaks if imported into server components without boundary isolation.
  Mitigation: Audit third-party dependencies during dependency updates to identify and encapsulate client-only imports behind local client boundary modules.
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
- Place the directive at the very top of the module file before any import declarations or executable logic.
- Push client boundaries as far down the component hierarchy as feasible, isolating interactive controls from static documentation content.
- Pass server-rendered content as children or component props into client boundary components to preserve server rendering benefits for static descendant nodes.

## Continuation Context


Verify commands:
- Discover the project dependency manifest and lock artifact, and verify the exact resolved versions of the UI framework and component libraries.
- Discover and run the project static analysis and linting scripts to verify that client hooks are accompanied by client boundary declarations.
- Discover and execute the project build verification command to confirm clean compilation across server and client component boundaries.

Accept when:
- All UI components utilizing React state, effects, browser DOM references, or client-only hooks declare the use client directive at the module root.
- Static and server-renderable UI components without interactivity remain free of the use client directive to avoid unnecessary client bundle growth.
- Automated build and static analysis checks pass with zero client boundary syntax or runtime lifecycle errors.

## Enforcement

- Verified by: Static analysis rules and linting checks configured in the continuous integration pipeline that flag client hook usage in modules lacking the directive.
- Verified by: Automated build verification ensuring no server-side execution failures occur due to browser API access.
- Verified by: Peer code review validating that client boundaries are placed as close to leaf nodes as possible.
- Violation handling: Build failures in continuous integration when client hooks or browser APIs are invoked without the directive.
- Violation handling: Rejection of pull requests introducing unnecessary client boundary directives on purely presentational components.
- Violation handling: Mandatory remediation of boundary leaks prior to deployment into production environments.
- Exception process: Submit an architectural exception request detailing why a client-dependent component cannot declare the boundary directive at module scope.
- Exception process: Review by frontend architectural stewards to evaluate alternatives such as dynamic imports or architectural restructuring.
- Exception process: Document approved exceptions with clear rationale and expiration conditions in the project repository.