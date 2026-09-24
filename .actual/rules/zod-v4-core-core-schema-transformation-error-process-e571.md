# Standard Schema Specification Module Adoption: Core Schema Transformation Error Processing Modules

These rules are ALWAYS ACTIVE for core schema transformation, serialization, and error processing modules.

### Rules

- **R-MOD-001** MUST: Core schema transformation and error processing modules MUST integrate and conform to the Standard Schema specification module for external interoperability and standardized validation contracts.

### Verify

```bash
# Discover and run the repository build, type verification, and automated test suite scripts as defined in the repository manifest.
```

**Accept when:**
- All core module static type checks and contract interface verifications pass without compilation or diagnostic errors.
- All automated test suites exercising schema transformation, error construction, and specification interoperability pass successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests and changes to core schema and error processing modules must be verified via static type analysis and test suites.
</enforcement>