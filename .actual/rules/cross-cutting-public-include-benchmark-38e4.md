# Adopt Structured Error Message Localization for Public API Validation: Public Include Benchmark

These rules are ALWAYS ACTIVE for all public validation API endpoints, exported functions, error message structures, localization modules, schema validation interfaces, and public type definitions exposed through the public API contract.

### Rules

- **R-PUB-001** SHOULD: Public APIs SHOULD include benchmark tests to verify performance characteristics remain within acceptable thresholds.
- **R-PUB-002** MUST: All locale modules MUST export consistent error message structures matching a canonical interface.
- **R-PUB-003** MUST: Error handling code MUST be separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts).
- **R-PUB-004** MUST: Public API exports MUST include structured error types and locale modules.
- **R-PUB-005** MUST: Locale files MUST be organized in a dedicated locales/ directory with ISO language code naming (e.g., ko.ts, pl.ts, kh.ts, mk.ts).
- **R-PUB-006** MUST: Pull requests adding new error codes MUST include translations for all supported locales.
- **R-PUB-007** MUST: Breaking changes to error structure MUST require a major version bump and API review.
- **R-PUB-008** SHOULD: TypeScript's type system SHOULD be used to enforce that all error codes are covered in each locale module.
- **R-PUB-009** SHOULD: Benchmark tests SHOULD cover validation primitives, real-world scenarios, and discriminated unions to track performance impact.

### Verify

```bash
# Verify locale module exports
grep -r "export.*locale" packages/zod/src/*/locales/ | wc -l

# Verify error handling separation
find packages/zod/src -name 'errors.ts' -o -name 'error*.ts' | xargs grep -l 'interface.*Error'

# Verify benchmark tests exist and pass
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
- All supported locales contain translations for all error codes
- Locale files follow ISO language code naming convention in dedicated locales/ directory

<enforcement>
Claude Code MUST NOT skip or defer verification. All rules in this file are mandatory for public API validation code. Violations trigger CI build failures and require API Architecture Team review before merge.
</enforcement>