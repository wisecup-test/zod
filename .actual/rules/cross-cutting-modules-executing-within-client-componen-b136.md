---
version: 2
name: cross-cutting-modules-executing-within-client-componen-b136
description: "Next.js Runtime Environment Variable Boundary Segregation: Modules Executing Within Client Component Boundaries"
metadata:
  actual:
    adr_id: b136f530-5382-4edd-8158-dc6932143128
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

# Next.js Runtime Environment Variable Boundary Segregation: Modules Executing Within Client Component Boundaries

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/app/og.png/**`, `packages/docs/components/**`, `packages/docs/loaders/**`, `packages/docs/pages/api/**`.

These rules are ALWAYS ACTIVE for all application modules, server route handlers, data loaders, and client components accessing environment variables or external service credentials.

### Rules

- **R-ENV-001** MUST_NOT: Modules executing within client component boundaries or containing client rendering directives MUST NOT reference un-prefixed environment variables or sensitive credentials.

### Verify

```bash
# Discover the project manifest and execute the configured static analysis scripts
# Example discovery and execution (adapt to project tooling):
if [ -f "package.json" ]; then
  npm run lint || npx eslint .
fi
```

**Accept when:**
- Static analysis confirms zero references to un-prefixed environment variables within client component modules.
- Server route handlers and data loaders successfully authorize external requests using server-scoped environment credentials without exposing them in response bodies.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated static analysis, bundle inspection, and peer code reviews.
</enforcement>