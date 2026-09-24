# drizzle-orm/pg-core Table Schema Definition: Database Table Definitions Declared Drizzle Orm

These rules are ALWAYS ACTIVE for relational database table schemas and column definitions within the application data layer.

### Rules

- **R-DRIZZLE-001** MUST: Database table definitions MUST be declared using the drizzle-orm/pg-core schema definition interface.

### Verify

```bash
# Discover the project test runner configuration and execute test suites targeting data modeling modules.
# Discover the repository type checking command and run it to verify static type conformity of schema declarations.
```

**Accept when:**
- All data modeling tests pass without failures.
- Type checking completes with zero diagnostic errors across schema definitions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration type checking and automated test pipelines enforce compliance.
</enforcement>