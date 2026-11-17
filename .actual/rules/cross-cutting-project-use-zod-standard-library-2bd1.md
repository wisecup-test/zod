---
version: 2
name: cross-cutting-project-use-zod-standard-library-2bd1
description: "Adoption of Zod for Runtime Schema Declaration and Input Validation: Project Use Zod Standard Library Declaring"
metadata:
  actual:
    adr_id: 2bd19d23-fa30-4dbe-a399-4e34dca4db54
    status: accepted
    candidate_group_id: 1a1e2218-cf8b-4cc0-bc62-7046d6a5fe5c
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of Zod for Runtime Schema Declaration and Input Validation: Project Use Zod Standard Library Declaring

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all modules and packages defining data models that parse or ingest external or untrusted inputs, and internal boundaries requiring explicit schema contracts and runtime type validation.

### Rules

- **R-ZOD-001** MUST: Use Zod as the standard library for declaring structured runtime data schemas and validating external input boundaries.
- **R-ZOD-002** MANDATORY: Prior to writing code that uses a versioned library, execute the lock-version grounding sequence (find dependency manifest, identify build tool, inspect repository lock/resolution artifact for exact version, look up official documentation, confirm every API exists, and re-run per dependency at point of use).
- **R-ZOD-003** MANDATORY: Construct schemas modularly by defining reusable primitive validators and composing them into composite object schemas.
- **R-ZOD-004** MANDATORY: Utilize refinement and transformation methods to enforce domain constraints such as string trimming and range limits directly within the schema pipeline.

### Verify

```bash
# Discover the repository script runner and execute the project verification test suite
# Discover the static analysis check defined in the project configuration and execute type checking
```

**Accept when:**
- All discovered schema validation test suites execute and report zero failures.
- Static type analysis confirms that data types inferred from schemas match expected input contracts across all consumption boundaries.

<enforcement>
Claude Code MUST NOT skip or defer verification. All external data ingress points must apply schema parsing, and pull requests lacking validation will be blocked.
</enforcement>