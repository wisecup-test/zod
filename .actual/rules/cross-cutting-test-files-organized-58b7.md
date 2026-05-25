# Adopt Vitest as Standard Testing Framework for TypeScript Projects: Test Files Organized

These rules are ALWAYS ACTIVE for all TypeScript test files and testing infrastructure within the monorepo.

### Rules

- **R-VITEST-001** MUST: Test files MUST be organized within a `tests/` directory at the appropriate package level.
- **R-VITEST-002** MUST: Test files MUST use the `.test.ts` extension for consistent test discovery.
- **R-VITEST-003** MUST: All TypeScript packages within the monorepo MUST use Vitest as the standard testing framework.
- **R-VITEST-004** SHOULD: A shared `vitest.config.ts` SHOULD be created at the workspace root and extended by individual packages to ensure consistent configuration across the monorepo.
- **R-VITEST-005** SHOULD: Test file templates SHOULD be established for common scenarios (unit tests, async tests, error handling) to accelerate test creation and maintain consistency.
- **R-VITEST-006** SHOULD: Package.json scripts SHOULD include `test`, `test:watch`, and `test:coverage` commands using Vitest CLI for consistent developer workflow.
- **R-VITEST-007** MAY: Legacy packages being migrated MAY temporarily use Jest until migration is complete (EXC-001).
- **R-VITEST-008** MAY: Specialized testing scenarios requiring framework-specific features not available in Vitest MAY use alternative frameworks (EXC-002).

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

<enforcement>
Claude Code MUST NOT skip or defer verification of test file organization, naming conventions, and Vitest configuration. All pull requests must pass CI pipeline test execution and code review checklist validation before merge.
</enforcement>