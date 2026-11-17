---
version: 2
name: cross-cutting-authentication-credentials-inkeep-cxkit-d82a
description: "@inkeep/cxkit-react Integration for Documentation Search and Chat: Authentication Credentials Inkeep Cxkit React Provided"
metadata:
  actual:
    adr_id: d82a5d71-f37e-475b-9ec7-149d88143f73
    status: accepted
    candidate_group_id: b85fcc00-74b9-4972-9289-84379d156c19
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# @inkeep/cxkit-react Integration for Documentation Search and Chat: Authentication Credentials Inkeep Cxkit React Provided

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for frontend documentation user interface components requiring search dialogs or floating assistant widgets.

### Rules

- **R-INKEEP-001** MUST: Authentication credentials for @inkeep/cxkit-react MUST be provided through public runtime environment configuration using NEXT_PUBLIC_INKEEP_KEY.

### Verify

```bash
# Discover and run the workspace lint script to verify client boundary directives and environment variable usage.
# Discover and run the workspace typecheck script to validate component bindings against library interfaces.
# Discover and run the workspace test runner to confirm documentation component mounting.
```

**Accept when:**
- Static analysis verification confirms all widget wrapper components declare client boundaries.
- Type checking completes with zero unresolved symbols or incompatible interface references.
- Component mounting tests verify proper configuration resolution and lifecycle initialization.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated pull request checks run repository linting and typecheck scripts, and code review validates client boundary declarations and credential exposure rules.
</enforcement>