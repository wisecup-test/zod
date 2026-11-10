---
version: 2
name: cross-cutting-before-implementing-updating-modules-tha-dfbd
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

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/app/og.png/**`, `packages/docs/components/**`, `packages/docs/loaders/**`, `packages/docs/pages/api/**`.

These rules are ALWAYS ACTIVE for all application modules, server route handlers, data loaders, and client components accessing environment variables or external service credentials.

### Rules

- **R-ENV-001** MUST: Before implementing or updating modules that rely on runtime framework dependencies, discover the ecosystem resolution artifact in the repository and verify the exact resolved dependency version against official documentation.
- **R-ENV-002** MUST: Ensure that components marked with client rendering directives only reference public environment variables.
- **R-ENV-003** MUST: Ensure server loaders and route handlers sanitize responses to avoid including raw environment objects or authorization headers in client payloads.

### Verify

```bash
# Discover the project manifest and execute static analysis scripts to verify no client components reference private environment variables
npm run lint
npm run test
```

**Accept when:**
- Static analysis confirms zero references to un-prefixed environment variables within client component modules.
- Server route handlers and data loaders successfully authorize external requests using server-scoped environment credentials without exposing them in response bodies.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>