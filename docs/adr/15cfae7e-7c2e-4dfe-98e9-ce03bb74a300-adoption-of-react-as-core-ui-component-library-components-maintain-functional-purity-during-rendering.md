---
version: 2
name: 15cfae7e-7c2e-4dfe-98e9-ce03bb74a300-adoption-of-react-as-core-ui-component-library-components-maintain-functional-purity-during-rendering
description: "Adoption of React as Core UI Component Library: Components Maintain Functional Purity During Rendering"
metadata:
  actual:
    adr_id: 15cfae7e-7c2e-4dfe-98e9-ce03bb74a300
    status: accepted
    candidate_group_id: b06f414d-38f9-4b85-bef7-5ca278d92919
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
      - components/**
      - loaders/**
---

# Adoption of React as Core UI Component Library: Components Maintain Functional Purity During Rendering

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `app/**`
- `components/**`
- `loaders/**`

## Context

- The documentation subsystem requires interactive presentation components including search dialogs, tabbed panels, copy buttons, and dynamic navigation outlines.
- Static analysis across sixteen documentation modules confirms universal adoption of React as the primary UI library for declarative view composition.
- Components consistently incorporate stateful hooks, DOM references, and client component boundary directives to coordinate user interface behavior.

## Problem Statement

Documentation user interfaces require a standardized component library to support declarative rendering, state management, and client-side lifecycle handling without fragmented presentation paradigms.

## Decision

1. SHOULD: Components SHOULD maintain functional purity during rendering by deferring non-rendering side effects to hook lifecycles.

## Policy Block

- SHOULD Components SHOULD maintain functional purity during rendering by deferring non-rendering side effects to hook lifecycles.

In scope:
- Documentation user interface components, layout templates, and interactive client widgets.
- Modules responsible for rendering documentation content, navigation hierarchies, and client dialogs.

Out of scope:
- Non-browser utility libraries, standalone build-time code generators, and server-only data transform scripts that do not produce interactive markup.

## Rationale

- Universal detection of React across all sixteen analyzed documentation files indicates an established architectural standard for view composition.
- Employing functional components with state and effect hooks isolates side effects and preserves predictable state transitions across interactive widgets.
- Standardizing component architecture on React ensures cohesive integration between layouts, content loaders, and dynamic UI elements.

## Consequences

Positive:
- Provides a unified, declarative component paradigm across all documentation interface modules.
- Enables composable UI patterns through structured hooks for state, references, and side effects.
- Facilitates modular composition across navigation controls, search interfaces, and content presentation.

Negative:
- Introduces client-side JavaScript runtime overhead and hydration requirements for interactive documentation components.
- Requires deliberate boundary separation between server-rendered layouts and client-interactive widgets.

## Alternatives

- Static markup generation without a client UI component library (rejected)
  Rejected because: Lacks declarative abstractions for interactive UI states such as search dialogs, tab switching, and dynamic table-of-contents tracking.
  When valid: Valid for static documentation pages requiring zero client-side DOM interactivity or state.
- Alternative reactive component framework (rejected)
  Rejected because: Incompatible with the established component dependencies and layout definitions observed across the documentation subsystem.
  When valid: Valid when authoring an isolated documentation portal with no dependency integration requirements.

## Risks

- Uncontrolled proliferation of client rendering boundaries leading to excessive client bundle sizes.
  Mitigation: Enforce review standards that restrict client directives strictly to components requiring stateful hooks or browser events.
  Owner: engineering team
- Memory leaks or synchronization issues from improper cleanup within lifecycle hooks.
  Mitigation: Require explicit cleanup callbacks within effect hooks and verify ref lifecycle mutations during code review.
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
- Organize components hierarchically, separating presentation components from client-side interactive controllers.
- Encapsulate DOM mutations and element measurement within dedicated references rather than issuing imperative document queries.

## Continuation Context


Verify commands:
- Discover the repository build script from the dependency manifest and execute the static type verification.
- Inspect project configuration to identify and run the static linter verifying component hook constraints and client directive compliance.

Accept when:
- All component modules pass static type checking without missing dependency declarations.
- Component lint verification passes with zero violations of hook rules and rendering boundary constraints.

## Enforcement

- Verified by: Automated continuous integration static analysis, linting, and type-checking suites.
- Verified by: Architectural review during pull request evaluation to verify component boundaries and hook lifecycles.
- Violation handling: Pull requests introducing direct DOM manipulation outside references or omitting required rendering boundaries are blocked until remediated.
- Exception process: Exceptions require documented architectural justification and formal approval from the engineering team leads.