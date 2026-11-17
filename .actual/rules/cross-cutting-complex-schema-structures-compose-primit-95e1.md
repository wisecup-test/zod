---
version: 2
name: cross-cutting-complex-schema-structures-compose-primit-95e1
description: "Adoption of Zod for Schema Definition and Safe Parse Validation: Complex Schema Structures Compose Primitive Validators"
metadata:
  actual:
    adr_id: 95e1b0ee-8196-4c60-ba1c-ab3ee31ce4db
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

# Adoption of Zod for Schema Definition and Safe Parse Validation: Complex Schema Structures Compose Primitive Validators

Scope: applies to `play.ts`, `scripts/**`.

These rules are ALWAYS ACTIVE for runtime data validation across scripts and operational entry points and schema definition and input boundary verification for untrusted data payloads.

### Rules

- **R-ZOD-001** SHOULD: Complex schema structures SHOULD compose primitive schema validators into object schemas rather than implementing custom parsing logic.

### Verify

```bash
# Discover the repository test runner from project configuration and execute the schema validation test suite.
# Run the project static analysis and linting scripts to verify compliance with non-throwing validation patterns.
```

**Accept when:**
- All schema validation tests execute and pass with zero unhandled exceptions.
- Input validation call sites use safeParse and handle validation failure cases explicitly.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>