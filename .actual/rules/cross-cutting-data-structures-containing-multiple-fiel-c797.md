---
version: 2
name: cross-cutting-data-structures-containing-multiple-fiel-c797
description: "Adoption of Zod for Runtime Schema Declaration and Input Validation: Data Structures Containing Multiple Fields Modeled"
metadata:
  actual:
    adr_id: c797ae3b-6399-497d-9892-1ca5cc99966e
    status: accepted
    candidate_group_id: 1a1e2218-cf8b-4cc0-bc62-7046d6a5fe5c
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of Zod for Runtime Schema Declaration and Input Validation: Data Structures Containing Multiple Fields Modeled

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all modules and packages defining data models that parse or ingest external or untrusted inputs, and internal boundaries requiring explicit schema contracts and runtime type validation.

### Rules

- **R-ZOD-001** SHOULD: Data structures containing multiple fields SHOULD be modeled using object schema declarations composed of primitive validator types.
- **R-ZOD-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and versions from the project repository.
- **R-ZOD-003** MANDATORY: Before writing code that uses a versioned library, execute the lock-version grounding sequence: find dependency manifest, identify build tool, inspect lock/resolution artifact for exact version, look up official documentation for that exact version, confirm APIs exist, and re-verify per dependency at point of use.
- **R-ZOD-004** MANDATORY: Construct schemas modularly by defining reusable primitive validators and composing them into composite object schemas.
- **R-ZOD-005** MANDATORY: Utilize refinement and transformation methods to enforce domain constraints such as string trimming and range limits directly within the schema pipeline.

### Verify

```bash
# Discover the project script runner and execute verification test suites and static type checking
# Example discovery/execution sequence:
if [ -f package.json ]; then
  npm test
  npm run typecheck || npx tsc --noEmit
fi
```

**Accept when:**
- All discovered schema validation test suites execute and report zero failures.
- Static type analysis confirms that data types inferred from schemas match expected input contracts across all consumption boundaries.

<enforcement>
Claude Code MUST NOT skip or defer verification. All external data ingress points must apply schema parsing, and violations in pull requests will be blocked.
</enforcement>