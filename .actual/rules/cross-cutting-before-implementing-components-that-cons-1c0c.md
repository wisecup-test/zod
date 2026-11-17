---
version: 2
name: cross-cutting-before-implementing-components-that-cons-1c0c
description: "@inkeep/cxkit-react Integration for Documentation Search and Chat: Before Implementing Components That Consume Inkeep"
metadata:
  actual:
    adr_id: 1c0c2044-bfe0-431a-96da-92dd7ff7a28e
    status: accepted
    candidate_group_id: b85fcc00-74b9-4972-9289-84379d156c19
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# @inkeep/cxkit-react Integration for Documentation Search and Chat: Before Implementing Components That Consume Inkeep

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for frontend documentation user interface components requiring search dialogs or floating assistant widgets.

### Rules

- **R-INKEEP-001** MUST: Before implementing components that consume @inkeep/cxkit-react, the consumer MUST inspect the repository lock artifact to determine the exact resolved dependency version and verify API compatibility against version-specific documentation.

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