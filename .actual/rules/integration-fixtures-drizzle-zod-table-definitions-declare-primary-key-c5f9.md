# drizzle-orm/pg-core Table Schema Definition: Table Definitions Declare Primary Key Constraints

These rules are ALWAYS ACTIVE for relational database table schemas and column definitions within the application data layer.

### Rules

- **R-DRIZZLE-001** MUST: Table definitions MUST declare primary key constraints using dedicated column builder functions provided by drizzle-orm/pg-core.

### Verify

```bash
# Discover the project test runner configuration and execute test suites targeting data modeling modules.
# Discover the repository type checking command and run it to verify static type conformity of schema declarations.
```

**Accept when:**
- All data modeling tests pass without failures.
- Type checking completes with zero diagnostic errors across schema definitions.

<enforcement>
Claude Code MUST NOT skip or defer verification. All data models must be verified via continuous integration type checking and automated test pipelines.
</enforcement>