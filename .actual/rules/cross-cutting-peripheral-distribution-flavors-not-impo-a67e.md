---
version: 2
name: cross-cutting-peripheral-distribution-flavors-not-impo-a67e
description: "Core Module Architecture for Shared Schema Primitives: Peripheral Distribution Flavors Not Import Directly"
metadata:
  actual:
    adr_id: a67e0ac5-884f-4911-93c6-dddce344eb5b
    status: accepted
    candidate_group_id: bec2016e-3f8a-44fb-95a3-11cf67256d04
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Core Module Architecture for Shared Schema Primitives: Peripheral Distribution Flavors Not Import Directly

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all internal schema distributions, flavor entrypoints, and shared utility modules within the library architecture.

### Rules

- **R-CORE-001** MUST_NOT: Peripheral distribution flavors MUST NOT import directly from sibling distribution flavors to access shared parsing or traversal logic.

### Verify

```bash
# Discover and execute the project boundary analysis check to confirm that all shared imports originate from the core module
# Discover and run the repository test and validation suite to verify that all distribution flavors successfully integrate with the core module
```

**Accept when:**
- Dependency boundary analysis passes with zero cross-flavor couplings and all shared traversal logic referencing the core module.
- Repository test suites execute successfully with all modules resolving core registry and utility contracts.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated boundary and module resolution checks enforce these rules in the continuous integration pipeline, and violations block pull requests.
</enforcement>