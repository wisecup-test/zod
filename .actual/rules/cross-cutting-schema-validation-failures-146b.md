# Adopt Schema-Based Validation as Primary Data Storage Gateway: Schema Validation Failures

These rules are ALWAYS ACTIVE for all data storage operations requiring validation, serialization, or schema enforcement at the application boundary layer, including write operations to primary datastores, data serialization/deserialization at storage boundaries, API request/response payloads that will be persisted, configuration data loaded from external sources before storage, and cache layer operations where data integrity is critical.

### Rules

- **R-SCHEMA-001** MUST: Schema validation failures MUST result in rejected write operations with descriptive error messages.

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
Claude Code MUST NOT skip or defer verification. All datastore write operations MUST pass through schema validation before persistence. Violations detected by CI/CD pipeline checks, code review process, static analysis tools, and runtime monitoring MUST be remediated or approved through the documented exception process before merge.
</enforcement>