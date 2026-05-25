# Adopt Structured Error Message Localization for Public API Validation: Coercion Schema Validation

These rules are ALWAYS ACTIVE for all public validation API endpoints, exported functions, error message structures, localization modules, schema validation and coercion interfaces, and public type definitions within the validation library.

### Rules

- **R-COERCE-001** MUST: Coercion and schema validation logic MUST be separated into distinct modules to maintain clear API boundaries.
- **R-COERCE-002** MUST: All locale modules MUST export consistent error message structures matching a canonical interface.
- **R-COERCE-003** MUST: Error handling code MUST be separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts).
- **R-COERCE-004** MUST: All error codes MUST have translations in all supported locales; missing translations MUST be caught by automated tests.
- **R-COERCE-005** MUST: Public API exports MUST include structured error types and locale modules.
- **R-COERCE-006** MUST: Breaking changes to error structure MUST require a major version bump and API review.
- **R-COERCE-007** SHOULD: Organize locale files in a dedicated locales/ directory with ISO language code naming (e.g., ko.ts, pl.ts, kh.ts, mk.ts).
- **R-COERCE-008** SHOULD: Use TypeScript's type system to enforce that all error codes are covered in each locale module.
- **R-COERCE-009** SHOULD: Maintain benchmark tests for validation primitives, real-world scenarios, and discriminated unions to track performance impact.
- **R-COERCE-010** MAY: Legacy v3 APIs may use different error structures for backward compatibility (EXC-001).
- **R-COERCE-011** MAY: Minimal/mini variants may omit certain locale support to reduce bundle size (EXC-002).

### Verify

```bash
# Verify locale module exports
grep -r "export.*locale" packages/zod/src/*/locales/ | wc -l

# Verify error handling separation
find packages/zod/src -name 'errors.ts' -o -name 'error*.ts' | xargs grep -l 'interface.*Error'

# Verify benchmark tests
npm run test:benchmarks -- --grep 'primitives|realworld|discriminatedUnion'

# Verify locale completeness
npm run test -- --grep 'locale.*complete'

# Verify error structure consistency
npm run test -- --grep 'error.*structure'
```

**Accept when:**
- All locale modules export consistent error message structures matching the canonical interface
- Error handling code is separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts)
- Benchmark tests pass with performance metrics within acceptable thresholds
- Public API exports include structured error types and locale modules
- TypeScript type checking confirms all error codes are covered in each locale module
- Unit tests verify error message structure consistency across all locales
- Integration tests validate public API error contracts
- CI build passes all locale completeness and consistency checks

<enforcement>
Claude Code MUST NOT skip or defer verification. All rules in this file are mandatory for code changes affecting public validation APIs, error message structures, localization modules, schema validation, and coercion interfaces. Violations MUST be caught by CI pipeline checks before merge.
</enforcement>