---
version: 2
name: cross-cutting-client-side-user-interface-components-663d
description: "Next.js Runtime Environment Variable Boundary Segregation: Client Side User Interface Components Requiring"
metadata:
  actual:
    adr_id: 663d6d09-0f46-428e-8b85-0f18cee73e62
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

# Next.js Runtime Environment Variable Boundary Segregation: Client Side User Interface Components Requiring

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/app/og.png/**`, `packages/docs/components/**`, `packages/docs/loaders/**`, `packages/docs/pages/api/**`.

These rules are ALWAYS ACTIVE for all application modules, server route handlers, data loaders, and client components accessing environment variables or external service credentials.

### Rules

- **R-ENV-001** SHOULD: Client-side user interface components requiring third-party service identifiers SHOULD access configuration exclusively through public environment identifiers resolved at build or bundle time.
- **R-ENV-002** MANDATORY: Components marked with client rendering directives MUST only reference public environment variables.
- **R-ENV-003** MANDATORY: Server loaders and route handlers MUST sanitize responses to avoid including raw environment objects or authorization headers in client payloads.

### Verify

```bash
# Discover the project manifest and execute the configured static analysis scripts to verify no client components reference private environment variables.
# Inspect repository automation workflows and run the test suite to validate that server data loaders inject authorization tokens only into server request headers.
```

**Accept when:**
- Static analysis confirms zero references to un-prefixed environment variables within client component modules.
- Server route handlers and data loaders successfully authorize external requests using server-scoped environment credentials without exposing them in response bodies.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>