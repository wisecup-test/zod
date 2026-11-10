---
version: 2
name: cross-cutting-components-handling-untrusted-input-hand-fa1d
description: "Adoption of Zod for Schema Definition and Safe Parse Validation: Components Handling Untrusted Input Handle Safeparse"
metadata:
  actual:
    adr_id: fa1d57e2-1556-4d98-a8bb-1ad17d80f8f1
    status: accepted
    candidate_group_id: b4f55bd5-a322-4c04-b31c-7702542d2a0c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - play.ts
      - scripts/**
---

# Adoption of Zod for Schema Definition and Safe Parse Validation: Components Handling Untrusted Input Handle Safeparse

Scope: applies to `play.ts`, `scripts/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: Components handling untrusted input MUST handle safeParse validation failures explicitly by inspecting the result success discriminator.

### Verify

```bash
# Discover the repository test runner from project configuration and execute the schema validation test suite.
# Run the project static analysis and linting scripts to verify compliance with non-throwing validation patterns.
```

**Accept when:**
- All schema validation tests execute and pass with zero unhandled exceptions.
- Input validation call sites use safeParse and handle validation failure cases explicitly.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>