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

These rules are ALWAYS ACTIVE for:
- All application modules, server route handlers, data loaders, and client components accessing environment variables or external service credentials.

### Rules

- **R-SC-001** SHOULD: Client-side user interface components requiring third-party service identifiers SHOULD access configuration exclusively through public environment identifiers resolved at build or bundle time.

### Verify

- Discover the project manifest and execute the configured static analysis scripts to verify no client components reference private environment variables.
- Inspect repository automation workflows and run the test suite to validate that server data loaders inject authorization tokens only into server request headers.

**Accept when:**

- Static analysis confirms zero references to un-prefixed environment variables within client component modules.
- Server route handlers and data loaders successfully authorize external requests using server-scoped environment credentials without exposing them in response bodies.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis and bundle inspection in continuous integration pipelines.
- Verified by: Architectural and peer code reviews for any pull request touching environment variable access or external service authentication.
- Violation handling: Continuous integration checks block pull requests referencing un-prefixed environment variables in client modules.
- Violation handling: Security alerts trigger immediate remediation and credential rotation if private secrets are detected in build outputs.
- Exception process: Exceptions require formal architectural review and security team sign-off, documenting the operational justification and risk mitigations.
</enforcement>
