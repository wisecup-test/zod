# Adopt Vitest as Standard Testing Framework for TypeScript Projects: Testing Framework Support

These rules are ALWAYS ACTIVE for all TypeScript test files and testing infrastructure within the monorepo, including unit tests, integration tests, and test configuration files.

### Rules

- **R-VITEST-001** MUST: Testing framework MUST support async/await patterns for asynchronous test scenarios.
- **R-VITEST-002** MUST: All test files MUST use the `.test.ts` extension for consistent test discovery and organization.
- **R-VITEST-003** MUST: Test files MUST be organized within package-specific `tests/` directories aligned with package boundaries.
- **R-VITEST-004** MUST: Vitest configuration MUST be defined at workspace root (`vitest.config.ts`) and may be extended by individual packages.
- **R-VITEST-005** MUST: Package.json scripts MUST include `test`, `test:watch`, and `test:coverage` commands using Vitest CLI.
- **R-VITEST-006** SHOULD: Test files SHOULD import test utilities from 'vitest' (e.g., `describe`, `it`, `expect`).
- **R-VITEST-007** SHOULD: Developers SHOULD use test file templates for common scenarios (unit tests, async tests, error handling) to maintain consistency.
- **R-VITEST-008** MAY: Specialized testing scenarios requiring framework-specific features not available in Vitest may use alternative tools with documented justification.

### Verify

```bash
# Find test files with .test.ts extension
find . -name '*.test.ts' -type f | head -5

# Check for Vitest imports in test files
grep -r "from 'vitest'" --include='*.test.ts' | head -3

# Verify vitest.config.ts exists
test -f vitest.config.ts && echo 'Vitest config found' || echo 'Vitest config missing'

# Verify Vitest is installed as a dependency
npm list vitest 2>/dev/null || pnpm list vitest 2>/dev/null || yarn list vitest 2>/dev/null

# Verify package.json contains test scripts
grep -E '"test":|"test:watch":|"test:coverage":' package.json
```

**Accept when:**
- Test files with `.test.ts` extension are found in `tests/` directories within packages
- Vitest imports are present in test files (e.g., `import { describe, it, expect } from 'vitest'`)
- `vitest.config.ts` configuration file exists at workspace or package level
- Vitest is listed as a dependency in `package.json` and can be executed via npm/pnpm/yarn scripts
- Package.json scripts include `test`, `test:watch`, and `test:coverage` commands using Vitest

<enforcement>
Claude Code MUST NOT skip or defer verification. All test files must conform to R-VITEST-001 through R-VITEST-007. Violations trigger automated CI checks and code review feedback. Exceptions require architecture review board approval and must be documented with expiration dates.
</enforcement>