---
version: 2
name: cross-cutting-components-not-reference-browser-global-352a
description: "React Client Component Interaction Architecture: Components Not Reference Browser Global Objects"
metadata:
  actual:
    adr_id: 352a4d32-ca4c-4ac2-8b36-c58333a8a8b5
    status: accepted
    candidate_group_id: f9a2d8cc-8daa-42ab-90ec-25b61d21e072
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Client Component Interaction Architecture: Components Not Reference Browser Global Objects

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all interactive UI components authoring client-side state, DOM manipulation, or third-party client integrations in frontend documentation packages.

### Rules

- **R-CLIENT-001** MUST_NOT: Components MUST NOT reference browser global objects or perform DOM mutations outside of client lifecycle hooks or client event handlers.

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
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines, peer code review, and automated checks strictly enforce component boundary placement, effect cleanup logic, and client directive requirements.
</enforcement>