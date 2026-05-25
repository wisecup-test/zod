# Adopt Schema-Based Validation as Primary Data Storage Gateway: Data Written Primary

These rules are ALWAYS ACTIVE for all data storage operations requiring validation, serialization, or schema enforcement at the application boundary layer.

### Rules

- **R-DATA-001** MUST: All data written to primary datastores MUST pass through schema validation using Zod v4 or equivalent schema validation library.

### Verify

```bash
# Count .parse and safeParse calls in schema validation code
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
Claude Code MUST NOT skip or defer verification. All datastore write operations MUST be validated through schema validation before persistence. Violations block merge until schema validation is added or an approved exception is documented.
</enforcement>