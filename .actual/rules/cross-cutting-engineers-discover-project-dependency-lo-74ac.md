---
version: 2
name: cross-cutting-engineers-discover-project-dependency-lo-74ac
description: "Adoption of Zod for Schema Definition and Safe Parse Validation: Engineers Discover Project Dependency Lock Artifact"
metadata:
  actual:
    adr_id: 74aca23d-28f7-465d-a1c3-1fe1893158d1
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

# Adoption of Zod for Schema Definition and Safe Parse Validation: Engineers Discover Project Dependency Lock Artifact

Scope: applies to `play.ts`, `scripts/**`.

These rules are ALWAYS ACTIVE for runtime data validation across scripts, operational entry points, and untrusted data payloads.

### Rules

- **R-ZOD-001** MUST: Discover the project dependency lock artifact and verify the exact resolved version of Zod prior to implementing or modifying schema definitions.
- **R-ZOD-002** MUST: Construct schemas using primitive and composite definitions and validate incoming payloads with safeParse.
- **R-ZOD-003** MUST: Branch conditionally on the success property of the safeParse result object before accessing parsed values.

### Verify

```bash
# Discover the project dependency manifest and lock artifact, and run the schema validation test suite using the repository test runner
# Run project static analysis and linting scripts to verify compliance with non-throwing validation patterns
```

**Accept when:**
- All schema validation tests execute and pass with zero unhandled exceptions.
- Input validation call sites use safeParse and handle validation failure cases explicitly.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests introducing throwing parse methods or unvalidated inputs are rejected during code review.
</enforcement>