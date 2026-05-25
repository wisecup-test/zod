# Adopt Schema-Based Validation as Primary Data Storage Gateway: Schema Definitions Tested

These rules are ALWAYS ACTIVE for all data storage operations requiring validation, serialization, or schema enforcement at the application boundary layer, including write operations to primary datastores, data serialization/deserialization at storage boundaries, API request/response payloads that will be persisted, configuration data loaded from external sources before storage, and cache layer operations where data integrity is critical.

### Rules

- **R-SCHEMA-001** SHOULD: Schema definitions SHOULD be tested independently with dedicated test suites covering edge cases and validation rules.

### Verify

```bash
# Count parse/safeParse usage in Zod schema files
grep -r '\.parse\|safeParse' packages/zod/src --include='*.ts' | wc -l

# Find schema definition files using Zod
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
Claude Code MUST NOT skip or defer verification of schema validation presence in datastore operations. All new write operations to primary datastores require explicit schema validation or documented exception approval.
</enforcement>