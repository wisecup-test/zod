---
version: 2
name: cross-cutting-interactive-callback-handlers-passed-pro-489f
description: "React Client Component Interaction Architecture: Interactive Callback Handlers Passed Props Referenced"
metadata:
  actual:
    adr_id: 489f1f49-a51b-48fd-8bdf-a6170faa42ed
    status: accepted
    candidate_group_id: f9a2d8cc-8daa-42ab-90ec-25b61d21e072
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Client Component Interaction Architecture: Interactive Callback Handlers Passed Props Referenced

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all interactive UI components authoring client-side state, DOM manipulation, or third-party client integrations in frontend documentation packages.

### Rules

- **R-RCC-001** SHOULD: Interactive callback handlers passed as props or referenced within effect dependency arrays SHOULD be memoized with the useCallback hook.
- **R-RCC-002** MANDATORY: Position client component boundaries at leaf nodes of the component hierarchy whenever possible to maximize server rendering coverage.
- **R-RCC-003** MANDATORY: Encapsulate third-party client integrations into dedicated wrapper components that manage initialization and teardown within localized effects.

### Verify

```bash
# Discover and run the workspace static analysis script from the project manifest
# Discover and run the project automated test script from the project manifest
# Discover and run the project type checking script from the project manifest
```

**Accept when:**
- All interactive UI components declare the client directive at the module root and pass static analysis without lint violations.
- All component interaction tests execute successfully with zero unhandled exceptions or effect lifecycle warnings.
- Static type checking completes with zero diagnostic errors across all client component files.

<enforcement>
Claude Code MUST NOT skip or defer verification. All interactive UI components must adhere to client component interaction and callback memoization requirements.
</enforcement>