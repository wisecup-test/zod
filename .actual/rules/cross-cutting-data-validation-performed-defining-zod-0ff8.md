---
version: 2
name: cross-cutting-data-validation-performed-defining-zod-0ff8
description: "Adoption of Zod for Schema Definition and Input Validation: Data Validation Performed Defining Zod Schemas"
metadata:
  actual:
    adr_id: 0ff8940a-c3b2-4fc4-8e19-961838dcc06d
    status: accepted
    candidate_group_id: d82ab627-4321-406c-a644-2305a03bee19
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of Zod for Schema Definition and Input Validation: Data Validation Performed Defining Zod Schemas

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all runtime input validation and payload parsing across module boundaries.

### Rules

- **R-ZOD-001** MUST: Data validation MUST be performed by defining Zod schemas and invoking parsing methods at module boundaries prior to data consumption.

### Verify

```bash
# Discover the project's verification and test scripts from the repository manifest and execute them.
# Execute the repository test suite to confirm that schema validation runs without errors across all module formats.
```

**Accept when:**
- All schema validation parsing logic executes successfully across all supported module targets.
- Repository verification scripts complete with zero exit codes and no schema parsing errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via continuous integration pipelines and peer code review.
</enforcement>