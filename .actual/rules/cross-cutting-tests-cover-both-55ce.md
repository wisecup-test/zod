# Adopt Vitest as Standard Testing Framework for TypeScript Projects: Tests Cover Both

These rules are ALWAYS ACTIVE for all TypeScript test files within the monorepo, particularly those in `tests/` directories across all packages (v3, v4/classic, v4/mini, v4/core) and any new test files created going forward.

### Rules

- **R-VITEST-001** SHOULD: Tests SHOULD cover both positive and negative scenarios, including error handling and edge cases.

### Verify

```bash
# Find test files with .test.ts extension
find . -name '*.test.ts' -type f | head -5

# Check for Vitest imports in test files
grep -r "from 'vitest'" --include='*.test.ts' | head -3

# Verify vitest.config.ts exists
test -f vitest.config.ts && echo 'Vitest config found' || echo 'Vitest config missing'

# Check Vitest is listed as a dependency
npm list vitest 2>/dev/null || pnpm list vitest 2>/dev/null || yarn list vitest 2>/dev/null
```

**Accept when:**
- Test files with `.test.ts` extension are found in `tests/` directories within packages
- Vitest imports are present in test files (e.g., `import { describe, it, expect } from 'vitest'`)
- `vitest.config.ts` configuration file exists at workspace or package level
- Vitest is listed as a dependency in `package.json` and can be executed via npm/pnpm/yarn scripts
- Tests demonstrate coverage of both positive and negative scenarios with error handling and edge cases

<enforcement>
Claude Code MUST NOT skip or defer verification. All test files MUST follow the Vitest standard and SHOULD include comprehensive test coverage of both success and failure paths. Violations are blocked by CI checks and require code review feedback or exception approval.
</enforcement>