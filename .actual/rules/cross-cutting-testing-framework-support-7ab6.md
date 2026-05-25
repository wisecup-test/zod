# Adopt Vitest as Standard Testing Framework for TypeScript Projects: Testing Framework Support

These rules are ALWAYS ACTIVE for all TypeScript test files and testing infrastructure within the monorepo, including unit tests, integration tests, and test configuration files.

### Rules

- **R-VITEST-001** MUST: Testing framework MUST support native TypeScript execution without requiring separate compilation steps.
- **R-VITEST-002** MUST: All test files MUST use the `.test.ts` extension for consistent test discovery and organization.
- **R-VITEST-003** MUST: Test files MUST be organized within package-specific `tests/` directories aligned with package boundaries.
- **R-VITEST-004** MUST: All TypeScript packages within the monorepo MUST use Vitest for unit tests, validation logic tests, schemas, and utilities.
- **R-VITEST-005** MUST: A shared `vitest.config.ts` MUST exist at the workspace root and be extended by individual packages to ensure consistent configuration across the monorepo.
- **R-VITEST-006** MUST: Package.json scripts MUST include `test`, `test:watch`, and `test:coverage` commands using Vitest CLI for consistent developer workflow.
- **R-VITEST-007** SHOULD: Test files SHOULD import from 'vitest' (e.g., `import { describe, it, expect } from 'vitest'`) rather than other testing frameworks.
- **R-VITEST-008** SHOULD: Test file templates for common scenarios (unit tests, async tests, error handling) SHOULD be established and maintained to accelerate test creation and maintain consistency.
- **R-VITEST-009** MAY: Legacy packages being migrated MAY temporarily use Jest until migration is complete (EXC-001).
- **R-VITEST-010** MAY: Specialized testing scenarios requiring framework-specific features not available in Vitest MAY use alternative frameworks with documented justification (EXC-002).

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
- Package.json scripts include `test`, `test:watch`, and `test:coverage` commands using Vitest

<enforcement>
Claude Code MUST NOT skip or defer verification. All test files must be validated against these rules during code review and CI pipeline execution. Pull requests with incorrectly named test files or non-standard testing frameworks must be blocked or require documented exceptions.
</enforcement>