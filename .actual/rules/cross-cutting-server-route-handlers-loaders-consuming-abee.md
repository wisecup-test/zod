---
version: 2
name: cross-cutting-server-route-handlers-loaders-consuming-abee
description: "Next.js Runtime Environment Variable Boundary Segregation: Server Route Handlers Loaders Consuming Runtime"
metadata:
  actual:
    adr_id: abeec9f3-4776-4955-b411-73675c1f19d8
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

# Next.js Runtime Environment Variable Boundary Segregation: Server Route Handlers Loaders Consuming Runtime

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/app/og.png/**`, `packages/docs/components/**`, `packages/docs/loaders/**`, `packages/docs/pages/api/**`.

These rules are ALWAYS ACTIVE for all application modules, server route handlers, data loaders, and client components accessing environment variables or external service credentials.

### Rules

- **R-ENV-001** SHOULD: Server route handlers and loaders consuming runtime environment variables SHOULD validate the presence of required configuration variables before initiating external client network requests.
- **R-ENV-002** MUST: Ensure that all components marked with client rendering directives only reference public environment variables.
- **R-ENV-003** MUST: Ensure server loaders and route handlers sanitize responses to avoid including raw environment objects or authorization headers in client payloads.

### Verify

```bash
# Discover the project manifest and execute the configured static analysis scripts to verify no client components reference private environment variables.
# Inspect repository automation workflows and run the test suite to validate that server data loaders inject authorization tokens only into server request headers.
```

**Accept when:**
- Static analysis confirms zero references to un-prefixed environment variables within client component modules.
- Server route handlers and data loaders successfully authorize external requests using server-scoped environment credentials without exposing them in response bodies.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and bundle inspection in continuous integration pipelines enforce these requirements.
</enforcement>