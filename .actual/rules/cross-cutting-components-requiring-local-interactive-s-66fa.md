---
version: 2
name: cross-cutting-components-requiring-local-interactive-s-66fa
description: "React Client Component Interaction Architecture: Components Requiring Local Interactive State Utilize"
metadata:
  actual:
    adr_id: 66fa0331-d6da-4da7-b869-4e5b393b76cf
    status: accepted
    candidate_group_id: f9a2d8cc-8daa-42ab-90ec-25b61d21e072
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Client Component Interaction Architecture: Components Requiring Local Interactive State Utilize

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-REACT-001** MUST: Components requiring local interactive state MUST utilize the useState hook to manage display and interaction states within the component boundary.

### Verify

```bash
# Discover and run static analysis script from project manifest
# Discover and run automated test script from project manifest
# Discover and run type checking script from project manifest
```

**Accept when:**
- All interactive UI components declare the client directive at the module root and pass static analysis without lint violations.
- All component interaction tests execute successfully with zero unhandled exceptions or effect lifecycle warnings.
- Static type checking completes with zero diagnostic errors across all client component files.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>