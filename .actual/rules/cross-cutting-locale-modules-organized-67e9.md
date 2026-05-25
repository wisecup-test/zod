# Adopt Structured Error Message Localization for Public API Validation: Locale Modules Organized

These rules are ALWAYS ACTIVE for all public validation API endpoints, exported functions, error message structures, localization modules, schema validation interfaces, and public type definitions within the scope of internationalized error handling and message formatting.

### Rules

- **R-LOCALE-001** SHOULD: Locale modules SHOULD be organized by ISO language codes (e.g., ko, pl, kh, mk) in dedicated locale directories.
- **R-LOCALE-002** MUST: All locale modules MUST export consistent error message structures matching a canonical interface.
- **R-LOCALE-003** MUST: Error handling code MUST be separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts).
- **R-LOCALE-004** MUST: All error codes MUST have translations in all supported locales; missing translations MUST be caught by TypeScript type checking.
- **R-LOCALE-005** MUST: Public API exports MUST include structured error types and locale modules.
- **R-LOCALE-006** MUST: Breaking changes to error structure MUST require a major version bump and API review.
- **R-LOCALE-007** SHOULD: New error codes SHOULD include translations for all supported locales before merge.
- **R-LOCALE-008** MAY: Legacy v3 APIs MAY use different error structures for backward compatibility (EXC-001).
- **R-LOCALE-009** MAY: Minimal/mini variants MAY omit certain locale support to reduce bundle size (EXC-002).

### Verify

```bash
# Count exported locale modules
grep -r "export.*locale" packages/zod/src/*/locales/ | wc -l

# Find error interface definitions
find packages/zod/src -name 'errors.ts' -o -name 'error*.ts' | xargs grep -l 'interface.*Error'

# Run benchmark tests for performance validation
npm run test:benchmarks -- --grep 'primitives|realworld|discriminatedUnion'

# Verify locale completeness using TypeScript type checking
npx tsc --noEmit

# Verify all error codes have translations in all supported locales
grep -r "export const" packages/zod/src/locales/*.ts | cut -d: -f2 | sort | uniq -c
```

**Accept when:**
- All locale modules export consistent error message structures matching the canonical interface
- Error handling code is separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts)
- Benchmark tests pass with performance metrics within acceptable thresholds
- Public API exports include structured error types and locale modules
- TypeScript type checking confirms all error codes are covered in each locale module
- No locale files are out of sync with error codes
- All supported locales have complete translation coverage

<enforcement>
Claude Code MUST NOT skip or defer verification. All locale modules MUST pass TypeScript type checking and benchmark tests before acceptance. CI build MUST fail if locale modules are incomplete or inconsistent. Pull requests adding new error codes MUST include translations for all supported locales.
</enforcement>