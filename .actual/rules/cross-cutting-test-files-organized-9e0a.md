# Adopt Vitest as Standard Testing Framework for TypeScript Projects: Test Files Organized

These rules are ALWAYS ACTIVE for all TypeScript test files and testing infrastructure within the monorepo.

### Rules

- **R-VITEST-001** MUST: Use `.test.ts` file extension for all test files.
- **R-VITEST-002** MUST: Organize test files within `tests/` directories aligned with package boundaries.
- **R-VITEST-003** MAY: Organize test files into subdirectories within `tests/` for complex packages with many test scenarios.
- **R-VITEST-004** MUST: Import test utilities from `vitest` (e.g., `describe`, `it`, `expect`).
- **R-VITEST-005** MUST: Configure Vitest via `vitest.config.ts` at workspace or package level.
- **R-VITEST-006** MUST: Include Vitest as a dependency in `package.json`.
- **R-VITEST-007** MUST: Provide `test`, `test:watch`, and `test:coverage` npm/pnpm/yarn scripts using Vitest CLI.
- **R-VITEST-008** SHOULD: Use shared `vitest.config.ts` at workspace root extended by individual packages for consistency.
- **R-VITEST-009** SHOULD: Create test file templates for common scenarios (unit tests, async tests, error handling).
- **R-VITEST-010** SHOULD: Support native TypeScript and ESM module patterns without additional transformation layers.

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
- Package.json scripts include `test`, `test:watch`, and `test:coverage` commands using Vitest CLI

<enforcement>
Claude Code MUST NOT skip or defer verification of these rules. All test files MUST conform to the `.test.ts` naming convention and Vitest import patterns. CI pipeline integration and code review enforcement are mandatory.
</enforcement>