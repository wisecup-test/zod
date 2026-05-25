# Adopt Zod Schema Validation for Runtime Type Safety: Failed Validations Return

These rules are ALWAYS ACTIVE for all TypeScript/JavaScript files handling external data inputs at system boundaries, including API endpoints, WebSocket handlers, configuration parsers, database query results from untrusted sources, third-party API responses, user-uploaded file content, and GraphQL resolvers.

### Rules

- **R-ZOD-001** MUST: Failed validations MUST return structured error messages without exposing internal system details or stack traces to external callers.

### Verify

```bash
# Count Zod schema usage across codebase
grep -r "z\.object\|z\.string\|z\.number" --include="*.ts" --include="*.tsx" | wc -l

# Count safeParse/parse invocations in non-test code
grep -r "safeParse\|parse" --include="*.ts" --include="*.tsx" packages/ | grep -v test | wc -l

# Run validation-focused tests
npm test -- --testPathPattern=".*\.test\.ts$" --testNamePattern="validation|schema|zod"
```

**Accept when:**
- All API endpoint handlers include Zod schema validation before processing request bodies
- Validation test coverage exceeds 80% for all schema definitions with edge cases tested
- Performance benchmarks show validation overhead under 5ms for typical request payloads
- Security scan confirms no unvalidated external inputs at system boundaries
- Error responses from failed validations contain no stack traces or internal implementation details

<enforcement>
Claude Code MUST NOT skip or defer verification. All new API endpoints, configuration parsers, and external data handlers MUST include Zod schema validation with structured error returns. CI pipeline MUST fail if validation coverage requirements are not met.
</enforcement>