---
version: 2
name: cross-cutting-project-adopt-zod-standard-library-7934
description: "Adoption of Zod for Schema Definition and Input Validation: Project Adopt Zod Standard Library Runtime"
metadata:
  actual:
    adr_id: 7934c41a-39d6-4560-9ac4-cb209fc3acd9
    status: accepted
    candidate_group_id: d82ab627-4321-406c-a644-2305a03bee19
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of Zod for Schema Definition and Input Validation: Project Adopt Zod Standard Library Runtime

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: Adopt Zod as the standard library for runtime data schema definition and input validation.
- **R-ZOD-002** MANDATORY: Execute the lock-version grounding procedure (find dependency manifest, identify build tool, inspect lock/resolution artifact, lookup official documentation for exact version, confirm APIs exist, and re-run per dependency at point of use) before writing code that uses a versioned library.
- **R-ZOD-003** MANDATORY: Declare validation schemas modularly so that schema definitions and parsing operations remain consistent across all module compilation formats.
- **R-ZOD-004** MANDATORY: Handle validation failures at boundaries by catching parsing errors and transforming them into structured domain errors.

### Verify

```bash
# Discover the project's verification and test scripts from the repository manifest and execute them
npm test
```

**Accept when:**
- All schema validation parsing logic executes successfully across all supported module targets.
- Repository verification scripts complete with zero exit codes and no schema parsing errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines, peer code reviews, and automated test suites enforce schema validation across all boundary inputs.
</enforcement>