---
version: 2
name: cross-cutting-component-side-effects-external-script-e18b
description: "@inkeep/cxkit-react Integration for Documentation Search and Chat: Component Side Effects External Script Integrations"
metadata:
  actual:
    adr_id: e18beb06-06f3-454a-970c-d8c4fd058828
    status: accepted
    candidate_group_id: b85fcc00-74b9-4972-9289-84379d156c19
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# @inkeep/cxkit-react Integration for Documentation Search and Chat: Component Side Effects External Script Integrations

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for frontend documentation user interface components requiring search dialogs or floating assistant widgets.

### Rules

- **R-IN-001** SHOULD: Component side effects and external script integrations for @inkeep/cxkit-react SHOULD synchronize within React useEffect hooks to maintain consistent client lifecycle boundaries.

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