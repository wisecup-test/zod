# React 'use client' Directive for Client Component Rendering Boundaries: Client Components That Interact Runtime Environment

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The application user interface contains interactive elements requiring local state management, side-effect subscriptions, and browser DOM interactions.
- The underlying framework rendering model defaults to server components, requiring explicit module-level directives to establish client runtime execution boundaries.
- Multiple documentation presentation components incorporate React state hooks, lifecycle side effects, and client-side navigation parameters.

## Problem Statement

Without explicit boundaries between server-evaluated components and client-executed components, modules requiring browser runtime primitives, interactive state management, and client side effects fail to bundle or execute properly in hybrid rendering architectures. A standardized policy is required to govern the placement of client component boundaries.

## Decision

1. SHOULD: Client components that interact with runtime environment configuration SHOULD access only public client-exposed variables and MUST NOT access server-only secrets.

## Policy Block

- SHOULD Client components that interact with runtime environment configuration SHOULD access only public client-exposed variables and MUST NOT access server-only secrets.

In scope:
- Interactive UI components utilizing React state hooks, lifecycle side effects, or browser DOM events
- Components wrapping third-party interactive client libraries

Out of scope:
- Static presentation components that render markup without client-side interactivity
- Server-side data acquisition utilities and server-evaluated layouts

Exceptions:
- EXC-52-001: A third-party layout component library requires client context throughout a subtree

## Rationale

- Declaring the 'use client' directive provides an explicit instruction to the module bundler, partitioning client-side code execution from server-rendered structures.
- Explicit client boundaries permit components that consume useState, useEffect, and client routing hooks to operate with full access to browser runtime APIs.
- Restricting client component directives to interactive leaves preserves performance advantages by preventing unnecessary inclusion of non-interactive code in client bundles.

## Consequences

Positive:
- Enables stateful client interactivity, event listeners, and browser lifecycle hooks across UI components.
- Establishes explicit bundler boundaries separating client-evaluated widgets from server-rendered structures.
- Minimizes total client JavaScript payload by restricting browser execution to designated leaf components.

Negative:
- Increases client JavaScript asset size for each component module included in the client bundle.
- Prevents direct access to server-only data stores and private environment variables within client component files.

## Alternatives

- Applying client component boundary directives uniformly across all UI components and layouts (rejected)
  Rejected because: Inflates client JavaScript bundle payloads unnecessarily and prevents server-side evaluation of static markup
  When valid: In purely client-rendered single-page architectures lacking server component infrastructure
- Relying on global browser script attachments and imperative DOM mutations without component boundaries (rejected)
  Rejected because: Breaks component encapsulation, invalidates declarative state synchronization, and bypasses bundler optimizations
  When valid: In legacy unbundled server templates with standalone script assets

## Risks

- Elevating client boundaries too high in the component hierarchy, resulting in bundle payload bloat.
  Mitigation: Isolate client directives to the lowest possible nodes in the component tree and evaluate bundle output via build verification.
  Owner: Engineering team
- Attempting to access server-side secrets or private configuration from within client component boundaries.
  Mitigation: Implement static analysis rules that prohibit server-only configuration access within client component files.
  Owner: Engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Place the 'use client' directive as the initial statement of the component file, preceding all imports and declarations.
- Isolate client boundary declarations to focused leaf components to avoid converting surrounding server components into client components.
- Wrap third-party interactive libraries requiring browser execution within dedicated boundary components rather than elevating ancestor layouts.

## Continuation Context


Verify commands:
- Discover the project dependency manifest to locate the build script, then execute the build command to verify that all client component boundaries bundle without compilation errors.
- Discover the static analysis configuration and run the lint script to confirm compliance with client component directive constraints.

Accept when:
- The project build script succeeds with all client component boundaries properly recognized without bundling or compilation errors.
- Static analysis checks pass with zero violations regarding missing client directives on stateful components or unauthorized access to server-only resources.

## Enforcement

- Verified by: Automated continuous integration build checks verifying client component bundling and compilation.
- Verified by: Static analysis linting rules verifying client boundary placement against hook and browser API usage.
- Verified by: Peer code review on all pull requests introducing or modifying user interface component modules.
- Violation handling: Continuous integration builds fail upon detecting stateful hook usage in modules lacking the required boundary directive.
- Violation handling: Pull requests containing improper boundary placements or unauthorized resource access are blocked from merging.
- Exception process: Submit an architectural review request detailing the specific technical requirement for an exception.
- Exception process: Obtain documented approval from the frontend architecture lead prior to merging elevated boundary definitions.