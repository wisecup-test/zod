---
version: 2
name: cross-cutting-applications-utilizing-next-runtime-envi-5deb
description: "Next.js Runtime Environment Variable Boundary Segregation: Applications Utilizing Next Runtime Environment Segregate"
metadata:
  actual:
    adr_id: 5deb6cfd-dfef-4bca-b201-58cfd21cc5a6
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

# Next.js Runtime Environment Variable Boundary Segregation: Applications Utilizing Next Runtime Environment Segregate

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/app/og.png/**`, `packages/docs/components/**`, `packages/docs/loaders/**`, `packages/docs/pages/api/**`.

These rules are ALWAYS ACTIVE for all application modules, server route handlers, data loaders, and client components accessing environment variables or external service credentials.

### Rules

- **R-ENV-001** MUST: Applications utilizing the Next.js runtime environment MUST segregate credential and configuration access across runtime boundaries by restricting client-facing environment access exclusively to identifiers carrying the public prefix convention while confining sensitive secrets and authorization tokens to server-only execution contexts.

### Verify

```bash
# Discover the project manifest and execute the configured static analysis scripts
# to verify no client components reference private environment variables.
# Inspect repository automation workflows and run the test suite to validate
# that server data loaders inject authorization tokens only into server request headers.
if [ -f "package.json" ]; then
  npm run --if-present lint
  npm test --if-present
fi
```

**Accept when:**
- Static analysis confirms zero references to un-prefixed environment variables within client component modules.
- Server route handlers and data loaders successfully authorize external requests using server-scoped environment credentials without exposing them in response bodies.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, bundle inspection, and architectural code reviews verify compliance.
</enforcement>