---
version: 2
name: dfbd51bb-4f9b-4439-8352-16612749a7dd-next-js-runtime-environment-variable-boundary-segregation-before-implementing-updating-modules-that-rely
description: "Next.js Runtime Environment Variable Boundary Segregation: Before Implementing Updating Modules That Rely"
metadata:
  actual:
    adr_id: dfbd51bb-4f9b-4439-8352-16612749a7dd
    status: accepted
    candidate_group_id: b1c09ed9-78f1-48f7-b794-971a47abf27e
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

# Next.js Runtime Environment Variable Boundary Segregation: Before Implementing Updating Modules That Rely

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

- Modern web applications combine server-rendered route handlers, server data loaders, and browser-executed client components within a unified application boundary.
- External service integrations require privileged API tokens for authentication during server-side data loading, while client-side interface widgets require public configuration keys to initialize client SDKs.
- Unchecked access to process environment variables in isomorphic codebases creates a critical risk of leaking secret credentials into public client JavaScript bundles.
- Segregating environment variable access by runtime execution boundary ensures secrets remain strictly within server environments while public identifiers can be safely injected into client components.

## Problem Statement

Applications combining server and client rendering require external service credentials for background data loading and public configuration keys for interactive client components. Without explicit architectural segregation, references to environment variables can inadvertently bundle sensitive credentials into client-facing artifacts, exposing authorization tokens to end users and third-party inspection.

## Decision

1. MUST: Before implementing or updating modules that rely on runtime framework dependencies, developers MUST discover the ecosystem resolution artifact in the repository and verify the exact resolved dependency version against official documentation.

## Policy Block

- MUST Before implementing or updating modules that rely on runtime framework dependencies, developers MUST discover the ecosystem resolution artifact in the repository and verify the exact resolved dependency version against official documentation.

In scope:
- All application modules, server route handlers, data loaders, and client components accessing environment variables or external service credentials.

Out of scope:
- Static documentation assets and build-time configuration files that execute solely during compilation or asset generation.

## Rationale

- Confining privileged credentials to server-only loaders and API routes ensures sensitive tokens cannot be bundled into client assets or inspected via browser developer tooling.
- Adopting the framework public prefix convention allows client components to receive non-sensitive configuration values deterministically without exposing internal infrastructure parameters.
- Direct header injection of authentication tokens within server-side fetch routines establishes clear audit boundaries for credential consumption.

## Consequences

Positive:
- Guarantees that sensitive secrets and tokens remain contained within isolated server execution environments.
- Clarifies data and configuration boundaries between client components and server loaders.
- Prevents accidental exposure of private infrastructure variables across client bundles.

Negative:
- Requires client components needing sensitive operations to route requests through server endpoints rather than calling external services directly.
- Increases cognitive overhead when coordinating configuration keys that must span both client and server domains.

## Alternatives

- Unified Client and Server Runtime Configuration Store (rejected)
  Rejected because: Merging all configuration into a shared runtime object risks exposing server secrets to client rendering bundles if property filtering fails.
  When valid: Valid only in fully server-side applications with no browser client bundle generation.
- Encrypted Token Delivery to Client Components (rejected)
  Rejected because: Delivering encrypted credentials to client runtimes requires distributing decryption keys to the client, undermining credential confidentiality.
  When valid: Valid in zero-trust browser architectures where ephemeral session tokens are explicitly scoped for direct browser-to-service communication.

## Risks

- Accidental omission of public prefix on a required client configuration variable causes undefined values at client runtime.
  Mitigation: Enforce build-time lint checks and runtime assertion guards for mandatory client configuration keys.
  Owner: engineering team
- Inadvertent reference to server secret variables inside shared utility files imported by both client and server components.
  Mitigation: Use boundary analysis tools to flag server environment variable access in shared or client-imported dependency trees.
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
- Verify that all components marked with client rendering directives only reference public environment variables.
- Ensure server loaders and route handlers sanitize responses to avoid including raw environment objects or authorization headers in client payloads.

## Continuation Context


Verify commands:
- Discover the project manifest and execute the configured static analysis scripts to verify no client components reference private environment variables.
- Inspect repository automation workflows and run the test suite to validate that server data loaders inject authorization tokens only into server request headers.

Accept when:
- Static analysis confirms zero references to un-prefixed environment variables within client component modules.
- Server route handlers and data loaders successfully authorize external requests using server-scoped environment credentials without exposing them in response bodies.

## Enforcement

- Verified by: Automated static analysis and bundle inspection in continuous integration pipelines.
- Verified by: Architectural and peer code reviews for any pull request touching environment variable access or external service authentication.
- Violation handling: Continuous integration checks block pull requests referencing un-prefixed environment variables in client modules.
- Violation handling: Security alerts trigger immediate remediation and credential rotation if private secrets are detected in build outputs.
- Exception process: Exceptions require formal architectural review and security team sign-off, documenting the operational justification and risk mitigations.