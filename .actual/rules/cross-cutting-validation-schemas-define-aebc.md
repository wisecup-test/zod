# Adopt Zod Schema Validation for Runtime Type Safety: Validation Schemas Define

These rules are ALWAYS ACTIVE for all TypeScript/JavaScript files handling external data inputs, API boundaries, configuration parsing, and user-submitted content.

### Rules

- **R-ZOD-001** MUST: Validation schemas MUST define explicit types and constraints for all expected fields, rejecting unknown properties by default.

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

<enforcement>
Claude Code MUST NOT skip or defer verification. All new API endpoints, configuration parsers, WebSocket handlers, and external data processors require explicit Zod schema validation. Violations block pull requests until validation coverage meets requirements.
</enforcement>