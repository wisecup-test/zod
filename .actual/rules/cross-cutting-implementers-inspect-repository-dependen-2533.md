---
version: 2
name: cross-cutting-implementers-inspect-repository-dependen-2533
description: "React Client Component Interaction Architecture: Implementers Inspect Repository Dependency Manifest Lock"
metadata:
  actual:
    adr_id: 253371f2-844f-4c2e-9b27-c21f812e9ec0
    status: accepted
    candidate_group_id: f9a2d8cc-8daa-42ab-90ec-25b61d21e072
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# React Client Component Interaction Architecture: Implementers Inspect Repository Dependency Manifest Lock

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for all interactive UI components authoring client-side state, DOM manipulation, or third-party client integrations in frontend documentation packages.

### Rules

- **R-REACT-001** MUST: Implementers MUST inspect the repository dependency manifest and lock artifact to determine the exact resolved version of React before invoking hook APIs.

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