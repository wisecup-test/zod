---
version: 2
name: cross-cutting-engineers-declare-runtime-data-validatio-fd02
description: "Adoption of Zod for Schema Definition and Safe Parse Validation: Engineers Declare Runtime Data Validation Schemas"
metadata:
  actual:
    adr_id: fd023a23-1c41-49c1-8500-11241d0341f4
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

# Adoption of Zod for Schema Definition and Safe Parse Validation: Engineers Declare Runtime Data Validation Schemas

Scope: applies to `play.ts`, `scripts/**`.

These rules are ALWAYS ACTIVE for runtime data validation across scripts, operational entry points, and untrusted data payloads.

### Rules

- **R-ZOD-001** MUST: Engineers MUST declare runtime data validation schemas using structural primitives and validate input boundaries using safeParse instead of throwing validation methods.

### Verify

```bash
# Discover and execute the project test suite and static analysis scripts via project configuration/package manifest
```

**Accept when:**
- All schema validation tests execute and pass with zero unhandled exceptions.
- Input validation call sites use safeParse and handle validation failure cases explicitly.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>