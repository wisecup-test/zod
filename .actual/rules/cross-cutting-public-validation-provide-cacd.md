# Adopt Structured Error Message Localization for Public API Validation: Public Validation Provide

These rules are ALWAYS ACTIVE for all public validation API endpoints, exported functions, error message structures, localization modules, schema validation interfaces, and public type definitions exposed to external API consumers.

### Rules

- **R-CACD-001** MUST: All public validation APIs MUST provide structured error messages with consistent schema including error code, message, and path information.
- **R-CACD-002** MUST: All locale modules MUST export consistent error message structures matching a canonical interface.
- **R-CACD-003** MUST: Error handling code MUST be separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts).
- **R-CACD-004** MUST: All error codes MUST have translations in all supported locales; missing translations MUST cause CI build failure.
- **R-CACD-005** MUST: Pull requests adding new error codes MUST include translations for all supported locales before merge.
- **R-CACD-006** MUST: Breaking changes to error structure MUST require a major version bump and API review.
- **R-CACD-007** MUST: Performance regressions beyond acceptable thresholds MUST trigger automatic review and investigation.
- **R-CACD-008** SHOULD: Organize locale files in a dedicated locales/ directory with ISO language code naming (e.g., ko.ts, pl.ts, kh.ts, mk.ts).
- **R-CACD-009** SHOULD: Use TypeScript's type system to enforce that all error codes are covered in each locale module.
- **R-CACD-010** SHOULD: Maintain benchmark tests for validation primitives, real-world scenarios, and discriminated unions to track performance impact.
- **R-CACD-011** MAY: Legacy v3 APIs may use different error structures for backward compatibility (EXC-001).
- **R-CACD-012** MAY: Minimal/mini variants may omit certain locale support to reduce bundle size (EXC-002).

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
find packages/zod/src/locales -name '*.ts' -exec grep -l 'export' {} \; | wc -l
```

**Accept when:**
- All locale modules export consistent error message structures matching the canonical interface
- Error handling code is separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts)
- Benchmark tests pass with performance metrics within acceptable thresholds
- Public API exports include structured error types and locale modules
- TypeScript type checking confirms all error codes are covered in each locale module
- All supported locales have complete translations for all error codes
- No performance regressions are detected in CI benchmark suite

<enforcement>
Claude Code MUST NOT skip or defer verification. All rules in this file are mandatory for public validation API code. Violations MUST cause CI build failure or require explicit exception approval from the API Architecture Team.
</enforcement>