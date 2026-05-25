# Adopt Vitest as Standard Testing Framework for TypeScript Projects: Testing Framework Provide

These rules are ALWAYS ACTIVE for all TypeScript test files and testing infrastructure within the monorepo.

### Rules

- **R-VITEST-001** MUST: All test files MUST use the `.test.ts` extension and be organized within `tests/` directories aligned with package boundaries.
- **R-VITEST-002** MUST: All test files MUST import test utilities from the `vitest` package (e.g., `import { describe, it, expect } from 'vitest'`).
- **R-VITEST-003** MUST: A `vitest.config.ts` configuration file MUST exist at the workspace root or package level to standardize testing configuration across the monorepo.
- **R-VITEST-004** MUST: Vitest MUST be listed as a dependency in `package.json` and executable via standard npm/pnpm/yarn scripts (`test`, `test:watch`, `test:coverage`).
- **R-VITEST-005** SHOULD: Testing framework SHOULD provide fast execution times suitable for watch mode during development.
- **R-VITEST-006** SHOULD: Test files SHOULD follow consistent naming conventions and be organized predictably to reduce cognitive load and accelerate test discovery.
- **R-VITEST-007** SHOULD: Shared test utilities and templates SHOULD be created for common scenarios (unit tests, async tests, error handling) to maintain consistency across packages.
- **R-VITEST-008** MAY: Legacy packages being migrated may temporarily use Jest until migration is complete (EXC-001).
- **R-VITEST-009** MAY: Specialized testing scenarios requiring framework-specific features not available in Vitest may use alternative frameworks (EXC-002).

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
- CI pipeline runs test suite on every pull request and verifies all tests pass
- Code review checklist includes verification of test file naming conventions and organization
- Automated linting rules check for `.test.ts` extension on test files
- Package.json scripts are validated to use Vitest commands rather than other test runners

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests with incorrectly named test files (not using `.test.ts`) are blocked by CI checks. Code review feedback is provided for tests not following the established directory structure. Tests using non-standard frameworks trigger automated comments suggesting migration to Vitest. Quarterly audits identify non-compliant test files and create migration tickets. Exceptions require approval via architecture review board with documented justification and expiration date.
</enforcement>