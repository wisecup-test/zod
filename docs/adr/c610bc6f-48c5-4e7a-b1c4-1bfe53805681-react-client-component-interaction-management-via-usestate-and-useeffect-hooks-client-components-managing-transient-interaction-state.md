# React Client Component Interaction Management via useState and useEffect Hooks: Client Components Managing Transient Interaction State

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Frontend user interfaces require responsive client-side behaviors including interactive toggles, asynchronous clipboard operations, and external search modal integrations.
- Architectural boundaries require clear separation between static server-rendered markup and interactive client-hydrated components.
- Standardizing on React client interaction primitives ensures predictable component lifecycle handling and eliminates uncoordinated imperative DOM mutations.

## Problem Statement

Interactive UI components require a standardized mechanism to manage transient component state, browser event listeners, and asynchronous lifecycle operations without introducing hydration mismatches or uncoordinated DOM mutations.

## Decision

1. MUST: Client components managing transient interaction state MUST utilize the useState hook rather than external mutable variables or imperative DOM properties.

## Policy Block

- MUST Client components managing transient interaction state MUST utilize the useState hook rather than external mutable variables or imperative DOM properties.

In scope:
- Frontend UI components requiring user interaction, transient local state, or browser lifecycle events
- Components integrating client-side browser capabilities including clipboard access, search dialogs, or DOM navigation

Out of scope:
- Static server components that render purely from input properties without client-side state or browser APIs
- Backend data access layers, API routes, and non-visual utility modules

## Rationale

- Using useState for localized component state guarantees unidirectional data flow and prevents out-of-band state mutation within the component tree.
- Encapsulating browser integrations and asynchronous lifecycles inside useEffect ensures deterministic execution and teardown across component lifecycles.
- Declaring explicit client boundaries isolates interactive behavior, allowing non-interactive components to avoid client runtime hydration.

## Consequences

Positive:
- Establishes a uniform, declarative interaction model across all frontend presentation components.
- Isolates browser-specific APIs and transient interaction state within designated client boundaries, keeping server rendering clean.
- Ensures deterministic cleanup of timers, event listeners, and subscriptions across component lifecycles.

Negative:
- Mandates client-side hydration for components declaring client boundaries, increasing JavaScript bundle size.
- Improperly specified dependency arrays in effect hooks can lead to stale state closures or unintentional re-render cycles.

## Alternatives

- Imperative DOM manipulation and manual browser event listener bindings (rejected)
  Rejected because: Bypasses declarative component lifecycles, risking memory leaks, inconsistent state synchronization, and hydration mismatches.
  When valid: Valid only in specialized low-level graphics or canvas rendering contexts where declarative state updates introduce prohibitive performance overhead.
- Global client-side application store for all local component interactions (rejected)
  Rejected because: Introduces unnecessary architectural coupling and excessive state boilerplate for transient component-level UI interactions.
  When valid: Valid when interaction state must be shared across disparate application routes or persisted across independent browsing sessions.

## Risks

- Omission of hook dependencies causing stale closures or infinite re-render loops.
  Mitigation: Enforce static analysis rules that validate effect dependency completeness and detect missing dependencies.
  Owner: Frontend engineering team
- Unnecessary client boundary declarations inflating client-side hydration bundles.
  Mitigation: Conduct peer reviews to ensure client boundaries and interaction hooks are restricted to genuinely stateful components.
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
- Always return an explicit cleanup function from useEffect when subscribing to browser events, intervals, or asynchronous streams.
- Encapsulate complex multi-step interaction logic or paired useState and useEffect routines into custom hooks to preserve component readability.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting verification scripts.
- Discover and run the component test suite verification scripts.
- Discover and run the project build verification script to validate client component compilation.

Accept when:
- Static analysis verification confirms zero warnings or errors regarding hook dependencies and component boundaries.
- All automated component tests covering interaction state changes and lifecycle side effects pass successfully.
- Project build verification succeeds without rendering boundary or hydration failures.

## Enforcement

- Verified by: Continuous integration pipelines running automated static analysis rules and component test suites
- Verified by: Peer code review verifying adherence to client boundary isolation and hook usage guidelines
- Violation handling: Pull requests containing static analysis violations or missing effect cleanup handlers are blocked from merging.
- Violation handling: Detected violations require refactoring to comply with declarative React hook standards prior to release.
- Exception process: Exemptions for imperative integrations require submission of an architectural exemption request detailing technical constraints.
- Exception process: Approval must be granted by principal frontend engineers before code integration.