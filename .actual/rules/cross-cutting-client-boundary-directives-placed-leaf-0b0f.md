---
version: 2
name: cross-cutting-client-boundary-directives-placed-leaf-0b0f
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

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for:
- All frontend UI components within the documentation and web interface packages requiring interactive state, DOM manipulation, or browser APIs.
- Integration wrapper components interfacing with client-only third-party UI widgets and search dialogs.

### Rules

- **R-RM-001** SHOULD: Client boundary directives SHOULD be placed at leaf-level interactive components to maximize server-rendered markup and minimize client bundle size.

### Verify

- Discover the project dependency manifest and lock artifact, and verify the exact resolved versions of the UI framework and component libraries.
- Discover and run the project static analysis and linting scripts to verify that client hooks are accompanied by client boundary declarations.
- Discover and execute the project build verification command to confirm clean compilation across server and client component boundaries.

**Accept when:**

- All UI components utilizing React state, effects, browser DOM references, or client-only hooks declare the use client directive at the module root.
- Static and server-renderable UI components without interactivity remain free of the use client directive to avoid unnecessary client bundle growth.
- Automated build and static analysis checks pass with zero client boundary syntax or runtime lifecycle errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Static analysis rules and linting checks configured in the continuous integration pipeline that flag client hook usage in modules lacking the directive.
- Verified by: Automated build verification ensuring no server-side execution failures occur due to browser API access.
- Verified by: Peer code review validating that client boundaries are placed as close to leaf nodes as possible.
- Violation handling: Build failures in continuous integration when client hooks or browser APIs are invoked without the directive.
- Violation handling: Rejection of pull requests introducing unnecessary client boundary directives on purely presentational components.
- Violation handling: Mandatory remediation of boundary leaks prior to deployment into production environments.
- Exception process: Submit an architectural exception request detailing why a client-dependent component cannot declare the boundary directive at module scope.
- Exception process: Review by frontend architectural stewards to evaluate alternatives such as dynamic imports or architectural restructuring.
- Exception process: Document approved exceptions with clear rationale and expiration conditions in the project repository.
</enforcement>
