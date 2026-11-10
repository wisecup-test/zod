---
version: 2
name: cross-cutting-refinements-format-constraints-declared-ec3a
description: "Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Refinements Format Constraints Declared Via Check"
metadata:
  actual:
    adr_id: ec3a1e86-a580-4e47-8d45-5a2e7bb53311
    status: accepted
    candidate_group_id: 4ecfb3a9-b029-42f8-9301-7d71eb684470
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Refinements Format Constraints Declared Via Check

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** SHOULD: Refinements and format constraints SHOULD be declared via the check method using discrete validator functions including minLength, maxLength, email, trim, and refine.

### Verify

```bash
# Discover the project dependency manifest and lock file to inspect resolved module entries
if [ -f "package.json" ]; then
  npm ls zod || pnpm ls zod || yarn ls zod
fi

# Execute the project automated test suite via the repository script runner
if [ -f "package.json" ]; then
  npm test || pnpm test || yarn test
fi

# Run the project static type checker and linter
if [ -f "package.json" ]; then
  npm run typecheck || npx tsc --noEmit
fi
```

**Accept when:**
- All schema validation invocations resolve through the modular functional entrypoint without importing monolithic packages.
- Input parsing tests successfully verify structural and constraint assertions using schema parse methods.
- Static analysis and type checking pass without errors across all modules declaring validation schemas.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>