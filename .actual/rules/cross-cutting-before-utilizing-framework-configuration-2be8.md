---
version: 2
name: cross-cutting-before-utilizing-framework-configuration-2be8
description: "Next.js Runtime Environment Variable Resolution: Before Utilizing Framework Configuration Interfaces Consumer"
metadata:
  actual:
    adr_id: 2be8fa32-e931-47da-8514-b4eda3e2a86d
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

# Next.js Runtime Environment Variable Resolution: Before Utilizing Framework Configuration Interfaces Consumer

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/app/og.png/**`, `packages/docs/components/**`, `packages/docs/loaders/**`, `packages/docs/pages/api/**`.

These rules are ALWAYS ACTIVE for all server routes, data loaders, and client UI components requiring runtime configuration or deployment metadata, and client-side components requiring external service integration keys.

### Rules

- **R-NEXT-001** MUST: Before utilizing framework configuration interfaces, the consumer MUST inspect the repository lock artifact to determine the authoritative resolved version of the runtime framework.

### Verify

```bash
# Discover and run the project's static analysis script to verify that no server-only environment variables are referenced within client component boundaries.
# Discover and execute the type-checking script to confirm ambient typing and presence handling for all process.env references.
# Discover and execute the automated test suite to ensure server routes and loaders handle absent environment variables gracefully.
```

**Accept when:**
- Static analysis passes with zero violations regarding client-side exposure of server environment variables.
- Type checking completes without errors across all modules dereferencing process.env properties.
- All route handlers and loaders execute successfully or handle omitted optional configuration gracefully.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>