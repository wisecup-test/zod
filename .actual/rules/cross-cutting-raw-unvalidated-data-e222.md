# Adopt Schema-Based Validation as Primary Data Storage Gateway: Raw Unvalidated Data

These rules are ALWAYS ACTIVE for all data storage operations requiring validation, serialization, or schema enforcement at the application boundary layer.

### Rules

- **R-SCHEMA-001** MUST_NOT: Raw, unvalidated data MUST NOT be persisted to primary datastores without schema validation.

### Verify

```bash
# Count schema validation usage across codebase
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
Claude Code MUST NOT skip or defer verification of schema validation presence in datastore operations. Violations must be caught during code review and CI/CD pipeline checks before merge.
</enforcement>