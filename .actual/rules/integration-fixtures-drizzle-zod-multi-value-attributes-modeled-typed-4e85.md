# drizzle-orm/pg-core Table Schema Definition: Multi Value Attributes Modeled Typed Array

These rules are ALWAYS ACTIVE for relational database table schemas and column definitions within the application data layer.

### Rules

- **R-DRIZZLE-001** SHOULD: Multi-value attributes SHOULD be modeled using typed array column builders rather than untyped serialized structures.

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