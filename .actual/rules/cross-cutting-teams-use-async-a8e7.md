# Adopt Zod Schema Validation for Runtime Type Safety: Teams Use Async

These rules are ALWAYS ACTIVE for all TypeScript/JavaScript codebases handling external data inputs, API boundaries, configuration parsing, and user-submitted content.

### Rules

- **R-ZOD-001** MAY: Teams MAY use async refinements for validation requiring external service calls (database lookups, API checks).

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
Claude Code MUST NOT skip or defer verification. All API endpoints receiving external requests, WebSocket message handlers, configuration file parsers, database query results from untrusted sources, third-party API responses, user-uploaded file content, and GraphQL resolvers MUST include Zod schema validation. Violations trigger CI pipeline failure and security team notification.
</enforcement>