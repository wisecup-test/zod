# Standard Schema Specification Module Adoption: Core Error Formatting Diagnostic Reporting Components

These rules are ALWAYS ACTIVE for all core library modules responsible for schema transformations, schema serialization, validation metadata export, error handling, and diagnostic reporting.

### Rules

- **R-STD-001** MUST: Core error formatting and diagnostic reporting components MUST align error output representations with the specifications defined in the Standard Schema module.

### Verify

```bash
# Discover and run the repository build and type verification script
# Discover and run the automated test suite execution script covering core schema transformation and error handling
```

**Accept when:**
- All core module static type checks and contract interface verifications pass without compilation or diagnostic errors.
- All automated test suites exercising schema transformation, error construction, and specification interoperability pass successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated CI pipelines executing static type analysis and test suites on every pull request, and peer code reviews by core library maintainers.
</enforcement>