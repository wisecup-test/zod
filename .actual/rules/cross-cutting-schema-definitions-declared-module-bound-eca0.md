# Valibot Modular Schema Validation Adoption: Schema Definitions Declared Module Boundaries Ensure

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VAL-001** SHOULD: Schema definitions SHOULD be declared at module boundaries to ensure strong static typing and runtime input parsing across consumer interfaces.
- **R-VAL-002** MANDATORY: Construct schemas using modular functional composition, importing only the specific validators and types required for each payload.
- **R-VAL-003** MANDATORY: Execute the lock-version grounding protocol (manifest -> build tool -> lock/resolution artifact -> documentation -> verification) before writing code that uses a versioned library.

### Verify

```bash
# Discover and run the project test runner from the dependency manifest
TEST_CMD=$(node -p "const p = require('./package.json'); Object.keys(p.scripts || {}).find(s => s.includes('test')) || 'npm test'")
npm run ${TEST_CMD#npm run }

# Discover and run the project build script to confirm tree-shaking and bundle generation
BUILD_CMD=$(node -p "const p = require('./package.json'); Object.keys(p.scripts || {}).find(s => s.includes('build')) || 'npm run build'")
npm run ${BUILD_CMD#npm run }
```

**Accept when:**
- All schema validation tests pass across packages importing the validation library.
- Production bundle analysis confirms that only imported validation primitives are included in target distribution artifacts.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks and peer code reviews verify modular import practices, schema boundary definitions, and bundle size metrics.
</enforcement>