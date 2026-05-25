# Adopt Zod Schema Validation for Runtime Type Safety: Complex Validation Logic

These rules are ALWAYS ACTIVE for all TypeScript/JavaScript files handling external data inputs, API boundaries, configuration parsing, and user-submitted content.

### Rules

- **R-ZOD-001** SHOULD: Complex validation logic SHOULD use Zod refinements and transformations to encode business rules within schemas.

### Verify

```bash
# Count Zod schema usage across codebase
grep -r "z\.object\|z\.string\|z\.number" --include="*.ts" --include="*.tsx" | wc -l

# Count safeParse and parse invocations (excluding tests)
grep -r "safeParse\|parse" --include="*.ts" --include="*.tsx" packages/ | grep -v test | wc -l

# Run validation-focused tests
npm test -- --testPathPattern=".*\.test\.ts$" --testNamePattern="validation|schema|zod"
```

**Accept when:**
- All API endpoint handlers include Zod schema validation before processing request bodies
- Validation test coverage exceeds 80% for all schema definitions with edge cases tested
- Performance benchmarks show validation overhead under 5ms for typical request payloads
- Security scan confirms no unvalidated external inputs at system boundaries

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis scanning for unvalidated external inputs at API boundaries is mandatory. Code review checklist must require Zod validation for all new endpoints. CI pipeline integration tests must validate schema coverage. Security audit reviews of validation patterns must occur quarterly. Pull requests are blocked until validation coverage meets requirements.
</enforcement>