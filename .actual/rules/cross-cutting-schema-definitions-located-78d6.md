# Adopt Schema-Based Validation as Primary Data Storage Gateway: Schema Definitions Located

These rules are ALWAYS ACTIVE for all data storage operations requiring validation, serialization, or schema enforcement at the application boundary layer.

### Rules

- **R-SCHEMA-001** MUST: Schema definitions MUST be co-located with or directly referenced by the modules that perform datastore operations.

### Verify

```bash
# Count schema validation usage patterns
grep -r '\.parse\|safeParse' packages/zod/src --include='*.ts' | wc -l

# Find schema definition files
find . -name 'schemas.ts' -o -name '*.schema.ts' | xargs grep -l 'z\.' | wc -l

# Run schema and validation tests
npm test -- --testPathPattern='schema|validation' --passWithNoTests
```

**Accept when:**
- All datastore write operations include schema validation calls (.parse or .safeParse) before persistence
- Schema definition files exist and are tested with dedicated test suites achieving >80% coverage
- CI pipeline includes schema validation tests that must pass before merge
- Code review checklist includes verification of schema validation for new datastore operations

<enforcement>
Claude Code MUST NOT skip or defer verification. All datastore operations must pass through schema validation before persistence, and violations must be caught by CI/CD pipeline checks and code review process.
</enforcement>