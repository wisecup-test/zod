---
version: 2
name: cross-cutting-consumer-discover-ecosystem-lock-artifac-5625
description: "Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Consumer Discover Ecosystem Lock Artifact Resolve"
metadata:
  actual:
    adr_id: 5625311d-65a4-4a81-87c3-05e57d222093
    status: accepted
    candidate_group_id: 4ecfb3a9-b029-42f8-9301-7d71eb684470
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Consumer Discover Ecosystem Lock Artifact Resolve

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all input validation layers, data parsing modules, and runtime schema definitions across the codebase.

### Rules

- **R-ZOD-001** MUST: The consumer MUST discover the ecosystem lock artifact and resolve the exact installed dependency version before implementation.
- **R-ZOD-002** MUST: Declare object structures using z.object with discrete primitive fields and attach validation rules via the check method to ensure individual validator functions remain tree-shakeable.
- **R-ZOD-003** MUST: Centralize schema definitions adjacent to data transfer contracts or boundary ingress points to ensure consistent parsing execution across consumers.

### Verify

```bash
# Discover the project dependency manifest and lock file to inspect declared and resolved entries for the schema validation library
find . -maxdepth 2 -name "package.json" -o -name "pnpm-lock.yaml" -o -name "package-lock.json" -o -name "yarn.lock"
# Execute the project automated test suite via the repository script runner to validate schema parsing assertions
npm test || yarn test || pnpm test
# Run the project static type checker and linter to ensure schema definitions adhere to functional entrypoint constraints
npm run lint || npx tsc --noEmit
```

**Accept when:**
- All schema validation invocations resolve through the modular functional entrypoint without importing monolithic packages.
- Input parsing tests successfully verify structural and constraint assertions using schema parse methods.
- Static analysis and type checking pass without errors across all modules declaring validation schemas.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>