# Adopt Structured Error Message Localization for Public API Validation: Public Contracts Maintain

These rules are ALWAYS ACTIVE for all public validation API endpoints, exported functions, error message structures, localization modules, schema validation interfaces, and public type definitions exposed to external API consumers.

### Rules

- **R-PUB-001** MUST: Public API contracts MUST maintain backward compatibility for error message structure when introducing new versions.

### Verify

```bash
# Verify locale modules export consistent error message structures
grep -r "export.*locale" packages/zod/src/*/locales/ | wc -l

# Verify error handling code is separated from validation logic
find packages/zod/src -name 'errors.ts' -o -name 'error*.ts' | xargs grep -l 'interface.*Error'

# Verify benchmark tests pass for performance-critical paths
npm run test:benchmarks -- --grep 'primitives|realworld|discriminatedUnion'
```

**Accept when:**
- All locale modules export consistent error message structures matching a canonical interface
- Error handling code is separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts)
- Benchmark tests pass with performance metrics within acceptable thresholds
- Public API exports include structured error types and locale modules
- All error codes have translations in all supported locales (ko, pl, kh, mk, and others)
- Semantic versioning is maintained; breaking changes to error structure require major version bump
- API version namespaces (v3, v4) are used to manage backward compatibility

<enforcement>
Claude Code MUST NOT skip or defer verification. All locale completeness checks, error structure consistency tests, and benchmark suite runs MUST pass before accepting changes to public API error contracts. Breaking changes to error message structure require explicit major version bump and API Architecture Team review.
</enforcement>