# Zod Core Internal Module Partitioning for Locale Definitions: Before Implementing Updating Any Dependency Library

These rules are ALWAYS ACTIVE for all implementation and maintenance of language locale modules and internal core module interface consumption within the validation library package.

### Rules

- **R-ZOD-001** MUST: Before implementing or updating any dependency on the library, the consumer MUST locate the repository dependency manifest and inspect the authoritative lock artifact to verify the exact resolved version.
- **R-ZOD-002** MUST: When creating a new locale module, import only the check descriptors, error types, and formatting utility helpers from the internal core submodules.
- **R-ZOD-003** MUST: Ensure all error messages parameterized with input values or type expectations use the standardized utility formatting functions rather than custom string concatenation.

### Verify

```bash
# Discover and execute the project localization test runner
TEST_CMD=$(npm run | grep -oE '(test:i18n|test:locales|test)' | head -n 1)
if [ -n "$TEST_CMD" ]; then npm run $TEST_CMD; else npm test; fi

# Discover and execute the project module boundary linter for static dependency analysis
LINT_CMD=$(npm run | grep -oE '(lint:deps|lint:boundaries|lint)' | head -n 1)
if [ -n "$LINT_CMD" ]; then npm run $LINT_CMD; fi

# Discover and execute the build script to verify bundle decoupling
BUILD_CMD=$(npm run | grep -oE '(build:prod|build)' | head -n 1)
if [ -n "$BUILD_CMD" ]; then npm run $BUILD_CMD; fi
```

**Accept when:**
- All locale definitions compile cleanly and pass their respective message formatting test cases.
- Dependency linting confirms that localization modules import only designated internal core submodules without circular dependencies.
- Module bundle inspection verifies that importing an individual locale dictionary does not pull in unreferenced schema parsers.

<enforcement>
Claude Code MUST NOT skip or defer verification. All locale modules must strictly adhere to internal core submodule partitioning, and all dependency updates require authoritative lock file verification.
</enforcement>