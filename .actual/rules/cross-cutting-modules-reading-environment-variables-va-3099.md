---
version: 2
name: cross-cutting-modules-reading-environment-variables-va-3099
description: "Next.js Runtime Environment Variable Resolution: Modules Reading Environment Variables Validate Value"
metadata:
  actual:
    adr_id: 3099ebcc-7cf0-4f69-8849-e419715c1c57
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

# Next.js Runtime Environment Variable Resolution: Modules Reading Environment Variables Validate Value

Scope: applies to `packages/docs/app/blog/**`, `packages/docs/app/og.png/**`, `packages/docs/components/**`, `packages/docs/loaders/**`, `packages/docs/pages/api/**`.

These rules are ALWAYS ACTIVE for all server routes, data loaders, client UI components, and files requiring runtime configuration or deployment metadata.

### Rules

- **R-ENV-001** SHOULD: Modules reading environment variables validate value presence or provide fallback defaults prior to passing configuration values to external client requests or service boundaries.
- **R-ENV-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-ENV-003** MANDATORY: Execute lock-version grounding in order before writing code that uses a versioned library: (1) find dependency manifest, (2) identify build tool, (3) inspect lock/resolution artifact for exact version, (4) look up official documentation for that exact version, (5) confirm every API/class/function exists in that version, (6) re-run per dependency at point of use for version-sensitive behavior.
- **R-ENV-004** MANDATORY: Define ambient type declarations for process.env properties within the project type configuration to ensure type safety across consumption sites.
- **R-ENV-005** MANDATORY: Ensure all client-targeted configuration uses the framework-specified public exposure prefix to allow bundler inlining during static generation.
- **R-ENV-006** MANDATORY: Isolate third-party authentication tokens within server-only execution boundaries such as route handlers and server loaders.

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