---
version: 2
name: cross-cutting-validation-schemas-not-throw-unhandled-25d7
description: "Adoption of Zod for Schema Definition and Safe Parse Validation: Validation Schemas Not Throw Unhandled Exceptions"
metadata:
  actual:
    adr_id: 25d73e08-89a3-440f-a505-bb7937d5f693
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

# Adoption of Zod for Schema Definition and Safe Parse Validation: Validation Schemas Not Throw Unhandled Exceptions

Scope: applies to `play.ts`, `scripts/**`.

These rules are ALWAYS ACTIVE for runtime data validation across scripts, operational entry points, and schema definition and input boundary verification for untrusted data payloads.

### Rules

- **R-ZOD-001** MUST_NOT: Validation schemas MUST NOT throw unhandled exceptions across module boundaries during runtime data parsing.

### Verify

```bash
# Discover the repository test runner from project configuration and execute the schema validation test suite.
# Run the project static analysis and linting scripts to verify compliance with non-throwing validation patterns.
```

**Accept when:**
- All schema validation tests execute and pass with zero unhandled exceptions.
- Input validation call sites use safeParse and handle validation failure cases explicitly.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks and peer code reviews.
</enforcement>