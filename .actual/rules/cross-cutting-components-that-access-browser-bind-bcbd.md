---
version: 2
name: cross-cutting-components-that-access-browser-bind-bcbd
description: "React Client Component Interaction Architecture: Components That Access Browser Bind Client"
metadata:
  actual:
    adr_id: bcbd15aa-d892-49f6-89a7-c6133c1390ae
    status: accepted
    candidate_group_id: f9a2d8cc-8daa-42ab-90ec-25b61d21e072
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Client Component Interaction Architecture: Components That Access Browser Bind Client

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all interactive UI components authoring client-side state, DOM manipulation, or third-party client integrations in frontend documentation packages.

### Rules

- **R-CLIENT-001** MUST: UI components that access browser APIs, bind client event listeners, or manage localized interaction state MUST declare the client directive at the top of the component module.

### Verify

```bash
# Discover and run the workspace static analysis script
# Discover and run the project automated test script
# Discover and run the project type checking script
```

**Accept when:**
- All interactive UI components declare the client directive at the module root and pass static analysis without lint violations.
- All component interaction tests execute successfully with zero unhandled exceptions or effect lifecycle warnings.
- Static type checking completes with zero diagnostic errors across all client component files.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>