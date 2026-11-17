---
version: 2
name: cross-cutting-before-implementing-modifying-schema-def-6900
description: "Adoption of Zod for Runtime Schema Declaration and Input Validation: Before Implementing Modifying Schema Definitions Developers"
metadata:
  actual:
    adr_id: 6900ae2f-8ed5-41bf-9d12-0ba5745b58ad
    status: accepted
    candidate_group_id: 1a1e2218-cf8b-4cc0-bc62-7046d6a5fe5c
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of Zod for Runtime Schema Declaration and Input Validation: Before Implementing Modifying Schema Definitions Developers

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all modules and packages defining data models that parse or ingest external or untrusted inputs, and internal boundaries requiring explicit schema contracts and runtime type validation.

### Rules

- **R-ZOD-001** MUST: Before implementing or modifying schema definitions, developers MUST inspect the repository dependency resolution artifacts to identify the exact locked version of the validation library and validate API compatibility against official documentation.

### Verify

```bash
# Discover the repository script runner and execute the project verification test suite
# Discover the static analysis check defined in the project configuration and execute type checking
```

**Accept when:**
- All discovered schema validation test suites execute and report zero failures.
- Static type analysis confirms that data types inferred from schemas match expected input contracts across all consumption boundaries.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>