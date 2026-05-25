# Adopt Vitest as Standard Testing Framework for TypeScript Projects: Test Files Named

These rules are ALWAYS ACTIVE for all TypeScript test files within the monorepo, particularly those in package-specific `tests/` directories across all package versions (v3, v4/classic, v4/mini, v4/core).

### Rules

- **R-VITEST-001** MUST: Test files MUST use the `.test.ts` extension to enable consistent test discovery and automated tooling integration.
- **R-VITEST-002** SHOULD: Test files SHOULD be named descriptively to indicate the feature or scenario being tested (e.g., `async-refinements.test.ts`, `error-utils.test.ts`).
- **R-VITEST-003** SHOULD: Test files SHOULD be organized within package-specific `tests/` directories aligned with package boundaries.
- **R-VITEST-004** MUST: Test files MUST use Vitest imports (e.g., `import { describe, it, expect } from 'vitest'`) rather than other testing frameworks.
- **R-VITEST-005** SHOULD: Test suites SHOULD cover diverse scenarios including async operations, refinements, error handling, localization, codecs, and standard schema compliance.

### Verify

```bash
# Find test files with .test.ts extension
find . -name '*.test.ts' -type f | head -5

# Verify Vitest imports are present in test files
grep -r "from 'vitest'" --include='*.test.ts' | head -3

# Check for vitest.config.ts at workspace or package level
test -f vitest.config.ts && echo 'Vitest config found' || echo 'Vitest config missing'

# Verify Vitest is listed as a dependency
npm list vitest 2>/dev/null || pnpm list vitest 2>/dev/null || yarn list vitest 2>/dev/null
```

**Accept when:**
- Test files with `.test.ts` extension are found in `tests/` directories within packages
- Vitest imports are present in test files (e.g., `import { describe, it, expect } from 'vitest'`)
- `vitest.config.ts` configuration file exists at workspace or package level
- Vitest is listed as a dependency in `package.json` and can be executed via npm/pnpm/yarn scripts
- Test file names are descriptive and indicate the feature or scenario being tested

<enforcement>
Claude Code MUST NOT skip or defer verification of these rules. All test files must conform to the `.test.ts` naming convention and use Vitest imports. Violations detected in code review or CI pipeline must be addressed before merge.
</enforcement>