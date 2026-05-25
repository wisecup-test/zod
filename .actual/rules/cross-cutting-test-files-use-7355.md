# Adopt Vitest as Standard Testing Framework for TypeScript Projects: Test Files Use

These rules are ALWAYS ACTIVE for all TypeScript test files within the monorepo, covering unit tests, integration tests, localization tests, and standard schema compliance tests across all packages.

### Rules

- **R-VITEST-001** MUST: All test files MUST use the .test.ts extension for TypeScript test files.
- **R-VITEST-002** MUST: Test files MUST be organized within package-specific test directories following the established modular testing strategy.
- **R-VITEST-003** MUST: Test files MUST use Vitest imports (e.g., `import { describe, it, expect } from 'vitest'`) rather than other testing frameworks.
- **R-VITEST-004** SHOULD: Projects SHOULD maintain a vitest.config.ts configuration file at the workspace or package level to ensure consistent configuration across the monorepo.
- **R-VITEST-005** SHOULD: Package.json scripts SHOULD include 'test', 'test:watch', and 'test:coverage' commands using Vitest CLI for consistent developer workflow.
- **R-VITEST-006** MAY: Legacy packages being migrated may temporarily use Jest until migration is complete (EXC-001).
- **R-VITEST-007** MAY: Specialized testing scenarios requiring framework-specific features not available in Vitest may use alternative tools (EXC-002).

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
- Test files with .test.ts extension are found in tests/ directories within packages
- Vitest imports are present in test files (e.g., `import { describe, it, expect } from 'vitest'`)
- vitest.config.ts configuration file exists at workspace or package level
- Vitest is listed as a dependency in package.json and can be executed via npm/pnpm/yarn scripts
- CI pipeline runs test suite on every pull request and verifies all tests pass
- Code review checklist includes verification of test file naming conventions and organization

<enforcement>
Claude Code MUST NOT skip or defer verification. All test files must conform to the .test.ts naming convention and use Vitest as the testing framework. Pull requests with incorrectly named test files or non-standard frameworks are blocked by CI checks. Exceptions require approval via architecture review board with documented justification and expiration date.
</enforcement>