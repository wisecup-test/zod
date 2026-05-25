# Adopt Schema-Based Validation as Primary Data Storage Gateway: Schemas Include Transformation

These rules are ALWAYS ACTIVE for all data storage operations requiring validation, serialization, or schema enforcement at the application boundary layer, including write operations to primary datastores, data serialization/deserialization at storage boundaries, API request/response payloads that will be persisted, configuration data loaded from external sources before storage, and cache layer operations where data integrity is critical.

### Rules

- **R-SCHEMA-001** MAY: Schemas MAY include transformation logic (e.g., `.transform()`, `.preprocess()`) for data normalization before storage.
- **R-SCHEMA-002** MUST: All write operations to primary datastores (databases, key-value stores, document stores) include schema validation calls (`.parse()` or `.safeParse()`) before persistence.
- **R-SCHEMA-003** MUST: Schema definition files exist and are tested with dedicated test suites achieving >80% coverage.
- **R-SCHEMA-004** MUST: CI pipeline includes schema validation tests that must pass before merge.
- **R-SCHEMA-005** SHOULD: Code review checklist includes verification of schema validation for new datastore operations.
- **R-SCHEMA-006** SHOULD: Export TypeScript types from schemas using `type MyType = z.infer<typeof mySchema>` to maintain single source of truth.
- **R-SCHEMA-007** SHOULD: Define schemas in a centralized `schemas/` directory or co-located with data access modules.
- **R-SCHEMA-008** SHOULD: Create comprehensive test suites for each schema covering valid inputs, invalid inputs, edge cases, default values, and transformations.
- **R-SCHEMA-009** SHOULD: Integrate schema validation into data access layer (repositories, DAOs, or ORM models) so all writes automatically pass through validation.

### Verify

```bash
# Count schema validation usage
grep -r '\.parse\|safeParse' packages/zod/src --include='*.ts' | wc -l

# Find schema definition files
find . -name 'schemas.ts' -o -name '*.schema.ts' | xargs grep -l 'z\.' | wc -l

# Run schema and validation tests
npm test -- --testPathPattern='schema|validation' --passWithNoTests
```

**Accept when:**
- All datastore write operations include schema validation calls (`.parse` or `.safeParse`) before persistence
- Schema definition files exist and are tested with dedicated test suites achieving >80% coverage
- CI pipeline includes schema validation tests that must pass before merge
- Code review checklist includes verification of schema validation for new datastore operations

<enforcement>
Claude Code MUST NOT skip or defer verification. Violations are caught by CI/CD pipeline checks, code review process with explicit checklist items, static analysis tools detecting unvalidated datastore writes, and regular architecture audits. Exception process requires developer submission with performance metrics or technical justification, tech lead and architecture review board evaluation within 2 business days, code comments documenting exceptions with ADR reference and expiration date, and quarterly exception registry review.
</enforcement>