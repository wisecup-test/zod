---
version: 2
name: cross-cutting-components-importing-inkeep-cxkit-react-7de5
description: "@inkeep/cxkit-react Integration for Documentation Search and Chat: Components Importing Inkeep Cxkit React Declare"
metadata:
  actual:
    adr_id: 7de5cba3-59f8-4314-b20b-64244362bf86
    status: accepted
    candidate_group_id: b85fcc00-74b9-4972-9289-84379d156c19
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# @inkeep/cxkit-react Integration for Documentation Search and Chat: Components Importing Inkeep Cxkit React Declare

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for frontend documentation user interface components requiring search dialogs or floating assistant widgets.

### Rules

- **R-INKEEP-001** MUST: All components importing @inkeep/cxkit-react MUST declare client rendering boundaries using the "use client" directive at the component file root.

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
Claude Code MUST NOT skip or defer verification. All pull requests introducing unapproved documentation search libraries or unvalidated client secrets must be blocked.
</enforcement>