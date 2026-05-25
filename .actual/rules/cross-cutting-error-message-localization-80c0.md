# Adopt Structured Error Message Localization for Public API Validation: Error Message Localization

These rules are ALWAYS ACTIVE for all public validation API endpoints, exported functions, error message structures, localization modules, schema validation interfaces, and public type definitions exposed to external API consumers.

### Rules

- **R-LOCALIZE-001** MUST: Error message localization MUST be implemented through separate locale modules that export standardized error message mappings.
- **R-LOCALIZE-002** MUST: All locale modules MUST export consistent error message structures matching a canonical interface to ensure consistency across all supported languages.
- **R-LOCALIZE-003** MUST: Error handling code MUST be separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts).
- **R-LOCALIZE-004** MUST: Locale files MUST be organized in a dedicated locales/ directory with ISO language code naming (e.g., ko.ts, pl.ts, kh.ts, mk.ts).
- **R-LOCALIZE-005** MUST: Pull requests adding new error codes MUST include translations for all supported locales.
- **R-LOCALIZE-006** MUST: Breaking changes to error structure MUST require a major version bump and API review.
- **R-LOCALIZE-007** SHOULD: Use TypeScript's type system to enforce that all error codes are covered in each locale module.
- **R-LOCALIZE-008** SHOULD: Implement automated tests that verify all error codes have translations in all supported locales.
- **R-LOCALIZE-009** SHOULD: Maintain benchmark tests for validation primitives, real-world scenarios, and discriminated unions to track performance impact.
- **R-LOCALIZE-010** MAY: Legacy v3 APIs may use different error structures for backward compatibility (EXC-001).
- **R-LOCALIZE-011** MAY: Minimal/mini variants may omit certain locale support to reduce bundle size (EXC-002).

### Verify

```bash
# Count exported locale modules
grep -r "export.*locale" packages/zod/src/*/locales/ | wc -l

# Find error interface definitions
find packages/zod/src -name 'errors.ts' -o -name 'error*.ts' | xargs grep -l 'interface.*Error'

# Run benchmark tests for performance validation
npm run test:benchmarks -- --grep 'primitives|realworld|discriminatedUnion'
```

**Accept when:**
- All locale modules export consistent error message structures matching the canonical interface
- Error handling code is separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts)
- Benchmark tests pass with performance metrics within acceptable thresholds
- Public API exports include structured error types and locale modules
- TypeScript type checking confirms all error codes are covered in each locale module
- All supported locales have complete translations for all error codes

<enforcement>
Claude Code MUST NOT skip or defer verification. CI build MUST fail if locale modules are incomplete or inconsistent. Performance regressions beyond threshold MUST trigger automatic review and investigation. Breaking changes to error structure MUST require major version bump and API review.
</enforcement>