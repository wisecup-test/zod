# drizzle-orm/pg-core Table Schema Definition: Before Implementing Schema Definitions Drizzle Orm

These rules are ALWAYS ACTIVE for all relational database table schemas and column definitions within the application data layer using drizzle-orm/pg-core.

### Rules

- **R-DRIZZLE-001** MUST: Before implementing schema definitions with drizzle-orm/pg-core, the consumer MUST inspect the repository lock artifact to determine the exact resolved dependency version and consult matching reference documentation.

### Verify

```bash
# Discover and run the project type checking command
# Discover and run the project test runner targeting data modeling modules
```

**Accept when:**
- All data modeling tests pass without failures.
- Type checking completes with zero diagnostic errors across schema definitions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>