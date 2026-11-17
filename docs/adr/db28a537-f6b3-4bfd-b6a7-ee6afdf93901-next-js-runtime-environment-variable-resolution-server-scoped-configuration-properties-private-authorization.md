---
version: 2
name: db28a537-f6b3-4bfd-b6a7-ee6afdf93901-next-js-runtime-environment-variable-resolution-server-scoped-configuration-properties-private-authorization
description: "Next.js Runtime Environment Variable Resolution: Server Scoped Configuration Properties Private Authorization"
metadata:
  actual:
    adr_id: db28a537-f6b3-4bfd-b6a7-ee6afdf93901
    status: accepted
    candidate_group_id: f2f70e81-e710-4ea9-8400-9184dfbd5769
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/blog/**
      - app/og.png/**
      - components/**
      - loaders/**
      - pages/api/**
---

# Next.js Runtime Environment Variable Resolution: Server Scoped Configuration Properties Private Authorization

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `app/blog/**`
- `app/og.png/**`
- `components/**`
- `loaders/**`
- `pages/api/**`

## Context

- The application requires access to deployment environment metadata, external service authentication tokens, and client widget configuration across multiple execution environments.
- Native framework environment variable resolution allows configuration to be defined via execution environment variables and dereferenced through the global process object.
- Client-side components require selective configuration exposure while preventing server credentials from leaking into public bundles.

## Problem Statement

Runtime configuration must be distributed across distinct server and client execution boundaries without exposing sensitive credentials or introducing unnecessary configuration library dependencies.

## Decision

1. MUST_NOT: Server-scoped configuration properties and private authorization tokens MUST NOT be evaluated within client components or declared with client-exposed prefixes.

## Policy Block

- MUST_NOT Server-scoped configuration properties and private authorization tokens MUST NOT be evaluated within client components or declared with client-exposed prefixes.

In scope:
- All server routes, data loaders, and client UI components requiring runtime configuration or deployment metadata.
- Client-side components requiring external service integration keys.

Out of scope:
- Build-time static content files that do not evaluate runtime variables.
- Pure utility functions that receive configuration parameters exclusively via function arguments.

## Rationale

- Direct evaluation of process.env aligns with native Next.js compile-time and runtime variable scoping, eliminating the overhead of dedicated configuration abstraction layers.
- The framework client prefix convention provides explicit structural separation between public client variables and private server credentials across component boundaries.
- Observed patterns across server loaders, image generation routes, and client search components demonstrate consistent adoption of native environment variable access across diverse execution targets.

## Consequences

Positive:
- Zero third-party library overhead for runtime configuration management.
- Seamless integration with deployment platform environment variable injection.
- Compile-time safety preventing un-prefixed server secrets from being bundled into client assets.

Negative:
- Absence of centralized schema validation can lead to runtime failures if required environment variables are undefined.
- Scattered process.env references make auditing active configuration dependencies across the codebase more difficult.
- Type definitions for ambient environment variables are not automatically generated or enforced without explicit ambient typing.

## Alternatives

- Centralized schema validation using an external schema parsing library (rejected)
  Rejected because: Adds additional bundle size and initialization overhead for a documentation repository with low configuration complexity.
  When valid: Valid when application configuration involves complex type coercion, nested structures, or strict startup crash-on-invalid requirements.
- Dedicated configuration service module abstracting process.env access (rejected)
  Rejected because: Introduces an unnecessary indirection layer when framework compilation already handles client and server variable isolation natively.
  When valid: Valid in multi-tenant or enterprise architectures requiring dynamic runtime configuration reloading.

## Risks

- Missing environment variables causing unhandled runtime exceptions or broken external integrations in deployed environments.
  Mitigation: Implement defensive existence checks and logging at points of consumption, particularly within server-side loaders.
  Owner: engineering team
- Accidental exposure of sensitive credentials through misnamed client prefixes.
  Mitigation: Enforce automated linting rules and code review checkpoints that flag client-side imports referencing non-public variables.
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
- Define ambient type declarations for process.env properties within the project type configuration to ensure type safety across consumption sites.
- Ensure all client-targeted configuration uses the framework-specified public exposure prefix to allow bundler inlining during static generation.
- Isolate third-party authentication tokens within server-only execution boundaries such as route handlers and server loaders.

## Continuation Context


Verify commands:
- Discover and run the project's static analysis script to verify that no server-only environment variables are referenced within client component boundaries.
- Discover and execute the type-checking script to confirm ambient typing and presence handling for all process.env references.
- Discover and execute the automated test suite to ensure server routes and loaders handle absent environment variables gracefully.

Accept when:
- Static analysis passes with zero violations regarding client-side exposure of server environment variables.
- Type checking completes without errors across all modules dereferencing process.env properties.
- All route handlers and loaders execute successfully or handle omitted optional configuration gracefully.

## Enforcement

- Verified by: Automated static analysis checks in the continuous integration pipeline.
- Verified by: Peer code review for all pull requests modifying environment variable usage.
- Violation handling: Continuous integration builds fail upon detection of server variables accessed within client components.
- Violation handling: Code reviews reject pull requests that dereference unvalidated environment variables without appropriate fallbacks.
- Exception process: Submit an architectural review request documenting why direct framework-level environment variable evaluation is insufficient for a given module.