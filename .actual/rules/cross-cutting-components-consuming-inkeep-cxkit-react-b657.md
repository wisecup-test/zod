---
version: 2
name: cross-cutting-components-consuming-inkeep-cxkit-react-b657
description: "@inkeep/cxkit-react Integration for Documentation Search and Chat: Components Consuming Inkeep Cxkit React Not"
metadata:
  actual:
    adr_id: b6577456-5a9d-4814-8e2e-e31c978c6f87
    status: accepted
    candidate_group_id: b85fcc00-74b9-4972-9289-84379d156c19
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# @inkeep/cxkit-react Integration for Documentation Search and Chat: Components Consuming Inkeep Cxkit React Not

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-INKEEP-001** MUST_NOT: Components consuming @inkeep/cxkit-react MUST NOT expose private API credentials or server-only secret tokens to the client environment.

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
Claude Code MUST NOT skip or defer verification.
</enforcement>