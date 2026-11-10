---
version: 2
name: cross-cutting-dom-measurements-external-widget-initial-c5ea
description: "React Client Component Interaction Architecture: Dom Measurements External Widget Initialization Browser"
metadata:
  actual:
    adr_id: c5ea0d97-43b5-4c86-8343-e10ea65fae30
    status: accepted
    candidate_group_id: f9a2d8cc-8daa-42ab-90ec-25b61d21e072
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Client Component Interaction Architecture: Dom Measurements External Widget Initialization Browser

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all interactive UI components authoring client-side state, DOM manipulation, or third-party client integrations in frontend documentation packages.

### Rules

- **R-DOM-001** MUST: DOM measurements, external widget initialization, and browser window subscriptions MUST be encapsulated inside useEffect hooks and MUST provide cleanup functions when subscriptions are created.

### Verify

```bash
# Discover the workspace static analysis script from the project manifest and run it
# Discover the project automated test script from the project manifest and execute it
# Discover the project type checking script from the project manifest and run it
```

**Accept when:**
- All interactive UI components declare the client directive at the module root and pass static analysis without lint violations.
- All component interaction tests execute successfully with zero unhandled exceptions or effect lifecycle warnings.
- Static type checking completes with zero diagnostic errors across all client component files.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>