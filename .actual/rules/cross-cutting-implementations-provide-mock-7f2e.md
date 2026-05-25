# Adopt Structured Error Message Localization for Public API Validation: Implementations Provide Mock

These rules are ALWAYS ACTIVE for all public validation API endpoints, exported functions, error message structures, localization modules, schema validation interfaces, and public type definitions across all supported API versions and variants.

### Rules

- **R-LOCALIZATION-001** MAY: API implementations MAY provide mock utilities for testing purposes to facilitate consumer integration testing.
- **R-LOCALIZATION-002** MUST: All locale modules export consistent error message structures matching a canonical interface.
- **R-LOCALIZATION-003** MUST: Error handling code be separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts).
- **R-LOCALIZATION-004** MUST: Organize locale files in a dedicated locales/ directory with ISO language code naming (e.g., ko.ts, pl.ts, kh.ts, mk.ts).
- **R-LOCALIZATION-005** MUST: Use TypeScript's type system to enforce that all error codes are covered in each locale module.
- **R-LOCALIZATION-006** MUST: Pull requests adding new error codes include translations for all supported locales.
- **R-LOCALIZATION-007** MUST: Breaking changes to error structure require major version bump and API review.
- **R-LOCALIZATION-008** SHOULD: Implement automated tests that verify all error codes have translations in all supported locales.
- **R-LOCALIZATION-009** SHOULD: Maintain benchmark suite to track performance impact of error handling and localization logic.
- **R-LOCALIZATION-010** SHOULD: Provide clear documentation on how to add new locales and maintain existing translations.

### Verify

```bash
# Count exported locale modules
grep -r "export.*locale" packages/zod/src/*/locales/ | wc -l

# Find error interface definitions
find packages/zod/src -name 'errors.ts' -o -name 'error*.ts' | xargs grep -l 'interface.*Error'

# Run benchmark tests for validation primitives, real-world scenarios, and discriminated unions
npm run test:benchmarks -- --grep 'primitives|realworld|discriminatedUnion'

# Verify locale completeness using TypeScript type checking
npm run type-check

# Run unit tests for error message structure consistency
npm run test -- --grep 'locale|error.*structure'

# Run integration tests for public API error contracts
npm run test:integration -- --grep 'error.*contract|api.*error'
```

**Accept when:**
- All locale modules export consistent error message structures matching the canonical interface
- Error handling code is separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts)
- Benchmark tests pass with performance metrics within acceptable thresholds
- Public API exports include structured error types and locale modules
- TypeScript type checking confirms all error codes are covered in each locale module
- Unit tests verify error message structure consistency across all locales
- Integration tests validate public API error contracts
- No performance regressions detected in benchmark suite

<enforcement>
Claude Code MUST NOT skip or defer verification. All locale completeness checks, error structure consistency tests, and benchmark validations MUST pass before accepting changes to public validation APIs, error handling, or localization modules.
</enforcement>