---
version: 2
name: cross-cutting-interactive-documentation-search-dialogs-fcad
description: "@inkeep/cxkit-react Integration for Documentation Search and Chat: Interactive Documentation Search Dialogs Assistant Bubbles"
metadata:
  actual:
    adr_id: fcad28d1-4ebd-4a5a-847b-5859092099a0
    status: accepted
    candidate_group_id: b85fcc00-74b9-4972-9289-84379d156c19
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# @inkeep/cxkit-react Integration for Documentation Search and Chat: Interactive Documentation Search Dialogs Assistant Bubbles

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for frontend documentation user interface components requiring search dialogs or floating assistant widgets.

### Rules

- **R-IN-001** MUST: Interactive documentation search dialogs and assistant bubbles MUST use @inkeep/cxkit-react as the standard component integration library.

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