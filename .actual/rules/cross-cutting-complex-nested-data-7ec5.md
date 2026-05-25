# Adopt Schema-Based Validation as Primary Data Storage Gateway: Complex Nested Data

These rules are ALWAYS ACTIVE for all data storage operations requiring validation, serialization, or schema enforcement at the application boundary layer, including write operations to primary datastores, data serialization/deserialization, API request/response payloads that will be persisted, configuration data loaded from external sources, and cache layer operations where data integrity is critical.

### Rules

- **R-SCHEMA-001** SHOULD: Complex nested data structures SHOULD use composed schemas rather than inline validation logic.

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
Claude Code MUST NOT skip or defer verification. All datastore write operations MUST include schema validation. Code review MUST verify schema validation presence before merge. CI pipeline MUST fail if new datastore operations lack schema validation or approved exception.
</enforcement>