---
version: 2
name: cross-cutting-runtime-input-validation-enforced-invoki-fc6f
description: "Adoption of Zod for Runtime Schema Declaration and Input Validation: Runtime Input Validation Enforced Invoking Parse"
metadata:
  actual:
    adr_id: fc6fc97a-ebc6-4032-8c25-51c72c357de8
    status: accepted
    candidate_group_id: 1a1e2218-cf8b-4cc0-bc62-7046d6a5fe5c
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of Zod for Runtime Schema Declaration and Input Validation: Runtime Input Validation Enforced Invoking Parse

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all modules and packages defining data models that parse or ingest external or untrusted inputs, as well as internal boundaries requiring explicit schema contracts and runtime type validation.

### Rules

- **R-ZOD-001** MUST: Runtime input validation MUST be enforced by invoking parse methods on declared schemas at data ingestion boundaries.

### Verify

\`\`\`bash
# Discover the project script runner and execute the verification test suite and static analysis check
# Example discovery flow:
# 1. Inspect package.json / project config for test and typecheck scripts
# 2. Run test suite:
npm test
# 3. Run type checking:
npm run typecheck
\`\`\`

**Accept when:**
- All discovered schema validation test suites execute and report zero failures.
- Static type analysis confirms that data types inferred from schemas match expected input contracts across all consumption boundaries.

<enforcement>
Claude Code MUST NOT skip or defer verification. All external data ingress points must apply schema parsing and be verified via automated test suites and static analysis.
</enforcement>