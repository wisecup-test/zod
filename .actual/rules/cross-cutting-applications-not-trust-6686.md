# Adopt Zod Schema Validation for Runtime Type Safety: Applications Not Trust

These rules are ALWAYS ACTIVE for all TypeScript/JavaScript codebases handling external data inputs, API boundaries, configuration parsing, and user-submitted content.

### Rules

- **R-ZVAL-001** MUST_NOT: Applications MUST NOT trust TypeScript type assertions as a substitute for runtime validation at security boundaries.

### Verify

```bash
# Count Zod schema usage patterns
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
Claude Code MUST NOT skip or defer verification. Violations are caught by CI pipeline static analysis, code review checklists, and security audits. Pull requests are blocked until validation coverage meets requirements.
</enforcement>