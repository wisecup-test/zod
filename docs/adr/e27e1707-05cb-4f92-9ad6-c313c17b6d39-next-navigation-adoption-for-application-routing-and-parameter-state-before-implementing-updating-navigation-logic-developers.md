# next/navigation Adoption for Application Routing and Parameter State: Before Implementing Updating Navigation Logic Developers

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Routing and navigation across documentation modules require consistent primitives for parameter extraction and transition handling.
- Documentation pages and client-side view components coordinate navigation state using modular imports rather than global window APIs.
- The next/navigation module provides unified routing interfaces that support both client-side interactivity and server-rendered route structures.

## Problem Statement

Inconsistent navigation handling and direct manipulation of browser history or window location objects lead to race conditions, hydration mismatches, and uncoordinated navigation state between server-rendered route pages and interactive client components. A unified routing module adoption is required to govern how components inspect search parameters and transition between paths.

## Decision

1. MUST: Before implementing or updating navigation logic, developers MUST inspect the workspace dependency manifest and package lock artifact to identify and verify the exact resolved version of the routing dependency against official documentation.

## Policy Block

- MUST Before implementing or updating navigation logic, developers MUST inspect the workspace dependency manifest and package lock artifact to identify and verify the exact resolved version of the routing dependency against official documentation.

In scope:
- All application modules, route pages, and interactive UI components that read query parameters or initiate route transitions.

Out of scope:
- Isolated utility libraries and domain logic modules that do not interact with user interface rendering or routing state.

Exceptions:
- EXC-20-001: External navigation targets require hard navigation outside of the application host boundary.

## Rationale

- The codebase demonstrates consistent adoption of next/navigation across both server-rendered page routes and interactive client components.
- Extracting parameters through standardized searchParams accessors preserves compatibility with framework hydration lifecycles and caching strategies.
- Restricting navigation primitives to a single authoritative module prevents divergent routing implementations and facilitates predictable navigation debugging.

## Consequences

Positive:
- Standardizes route and parameter handling across documentation routes and interactive components.
- Eliminates hydration divergence by relying on framework-native navigation hooks and parameter accessors.
- Maintains clean boundaries between server route components and interactive client components.

Negative:
- Tightly couples UI components and parameter extraction logic to the specific routing module vendor.
- Requires client components observing dynamic search parameters to manage client boundary isolation to avoid rendering suspension issues.

## Alternatives

- Direct browser window location and history manipulation (rejected)
  Rejected because: Bypasses framework rendering lifecycles, causing hydration mismatches and uncoordinated page re-renders.
  When valid: Valid only in standalone vanilla scripts operating outside of the component application runtime.
- Custom URL state management wrapper abstractions (rejected)
  Rejected because: Introduces unnecessary maintenance overhead and indirection over native framework navigation primitives.
  When valid: Valid when multi-framework runtime portability across heterogeneous platforms is required.

## Risks

- Upstream breaking changes in navigation hooks or parameter accessor interfaces during major framework upgrades.
  Mitigation: Adhere to the lock-version grounding policy and execute automated test suites prior to dependency version updates.
  Owner: Frontend Platform Team
- Unwrapped dynamic search parameter reads causing unexpected client boundary de-optimizations.
  Mitigation: Enforce static analysis rules and code review checkpoints to ensure proper client boundary isolation.
  Owner: Frontend Platform Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Discover the workspace dependency manifest to verify the routing library scope before introducing navigation utilities in new packages.
- Ensure client-side components using navigation hooks encapsulate parameter-driven side effects inside dedicated lifecycle callbacks.

## Continuation Context


Verify commands:
- Inspect the project dependency manifest and lock artifact to verify that the routing module is registered as a required dependency.
- Execute repository linting and static analysis scripts to confirm no forbidden window location or history references exist in UI modules.
- Run the project automated test suite to ensure that route transitions and parameter retrieval behave as expected without runtime warnings.

Accept when:
- All routing and parameter interactions import exclusively from next/navigation.
- No direct window location or browser history manipulations exist within application components.
- Static analysis and automated component validation suites pass without routing-related errors.

## Enforcement

- Verified by: Automated continuous integration checks including static analysis lint rules.
- Verified by: Pull request architectural peer reviews verifying module import compliance.
- Violation handling: Pull requests introducing direct browser navigation or unapproved routing libraries are blocked until remediated.
- Exception process: Submit an architectural review request outlining why framework routing primitives are insufficient, requiring approval from the technical leads.