# Adopt Structured Error Message Localization for Public API Validation: Error Handling Implementations

These rules are ALWAYS ACTIVE for all public validation API endpoints, exported functions, error message structures, localization modules, schema validation interfaces, and public type definitions within the validation library.

### Rules

- **R-ERRLOC-001** SHOULD: Error handling implementations SHOULD support both classic and minimal variants to accommodate different performance and bundle size requirements.
- **R-ERRLOC-002** MUST: All locale modules MUST export consistent error message structures matching a canonical interface.
- **R-ERRLOC-003** MUST: Error handling code MUST be separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts).
- **R-ERRLOC-004** MUST: All error codes MUST have translations in all supported locales; missing translations MUST be caught by automated tests.
- **R-ERRLOC-005** MUST: Public API exports MUST include structured error types and locale modules.
- **R-ERRLOC-006** SHOULD: Locale files SHOULD be organized in a dedicated locales/ directory with ISO language code naming (e.g., ko.ts, pl.ts, kh.ts, mk.ts).
- **R-ERRLOC-007** SHOULD: TypeScript's type system SHOULD be used to enforce that all error codes are covered in each locale module.
- **R-ERRLOC-008** MUST: Breaking changes to error structure MUST require a major version bump and API review.
- **R-ERRLOC-009** MUST: Pull requests adding new error codes MUST include translations for all supported locales.
- **R-ERRLOC-010** SHOULD: Benchmark tests SHOULD be maintained for validation primitives, real-world scenarios, and discriminated unions to track performance impact.
- **R-ERRLOC-011** MAY: Legacy v3 APIs MAY use different error structures for backward compatibility (EXC-001).
- **R-ERRLOC-012** MAY: Minimal/mini variants MAY omit certain locale support to reduce bundle size (EXC-002).

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
- CI build passes locale completeness validation
- All supported locales have complete translations for all error codes

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated CI pipeline checks for locale completeness using TypeScript type checking, unit tests verify error message structure consistency across all locales, integration tests validate public API error contracts, and benchmark suite runs in CI to detect performance regressions. Violations result in CI build failure.
</enforcement>