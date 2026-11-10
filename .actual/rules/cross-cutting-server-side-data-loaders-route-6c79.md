---
version: 2
name: cross-cutting-server-side-data-loaders-route-6c79
description: "Next.js Runtime Environment Variable Boundary Segregation: Server Side Data Loaders Route Handlers"
metadata:
  actual:
    adr_id: 6c795375-8322-4332-9db9-0363208d0a8a
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

# Next.js Runtime Environment Variable Boundary Segregation: Server Side Data Loaders Route Handlers

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/app/og.png/**`, `packages/docs/components/**`, `packages/docs/loaders/**`, `packages/docs/pages/api/**`.

These rules are ALWAYS ACTIVE for all application modules, server route handlers, data loaders, and client components accessing environment variables or external service credentials.

### Rules

- **R-ENV-001** MUST: Server-side data loaders and route handlers communicating with external services MUST inject sensitive authentication credentials directly within server-scoped request authorization headers without leaking values to client payloads.

### Verify

```bash
# Discover the project manifest and execute configured static analysis scripts
# to verify no client components reference private environment variables.
# Inspect repository automation workflows and run the test suite to validate
# that server data loaders inject authorization tokens only into server request headers.
```

**Accept when:**
- Static analysis confirms zero references to un-prefixed environment variables within client component modules.
- Server route handlers and data loaders successfully authorize external requests using server-scoped environment credentials without exposing them in response bodies.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>