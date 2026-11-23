---
version: 2
name: cross-cutting-server-scoped-configuration-properties-p-db28
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

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/app/og.png/**`, `packages/docs/components/**`, `packages/docs/loaders/**`, `packages/docs/pages/api/**`.

These rules are ALWAYS ACTIVE for:
- All server routes, data loaders, and client UI components requiring runtime configuration or deployment metadata.
- Client-side components requiring external service integration keys.

### Rules

- **R-CEM-001** MUST_NOT: Server-scoped configuration properties and private authorization tokens MUST NOT be evaluated within client components or declared with client-exposed prefixes.

### Verify

- Discover and run the project's static analysis script to verify that no server-only environment variables are referenced within client component boundaries.
- Discover and execute the type-checking script to confirm ambient typing and presence handling for all process.env references.
- Discover and execute the automated test suite to ensure server routes and loaders handle absent environment variables gracefully.

**Accept when:**

- Static analysis passes with zero violations regarding client-side exposure of server environment variables.
- Type checking completes without errors across all modules dereferencing process.env properties.
- All route handlers and loaders execute successfully or handle omitted optional configuration gracefully.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis checks in the continuous integration pipeline.
- Verified by: Peer code review for all pull requests modifying environment variable usage.
- Violation handling: Continuous integration builds fail upon detection of server variables accessed within client components.
- Violation handling: Code reviews reject pull requests that dereference unvalidated environment variables without appropriate fallbacks.
- Exception process: Submit an architectural review request documenting why direct framework-level environment variable evaluation is insufficient for a given module.
</enforcement>
