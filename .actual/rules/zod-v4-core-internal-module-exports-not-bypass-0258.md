# Standard Schema Specification Module Adoption: Internal Module Exports Not Bypass Standard

These rules are ALWAYS ACTIVE for core library modules responsible for schema transformations, schema serialization, validation metadata export, and core error handling/diagnostic reporting.

### Rules

- **R-STD-001** MUST_NOT: Internal module exports MUST NOT bypass the Standard Schema contract when exposing validation mechanisms intended for ecosystem consumption.

### Verify

```bash
# Discover and run the repository build and type verification script
# Discover and run the automated test suite execution script covering core schema transformation and error handling
```

**Accept when:**
- All core module static type checks and contract interface verifications pass without compilation or diagnostic errors.
- All automated test suites exercising schema transformation, error construction, and specification interoperability pass successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipelines executing static type analysis and test suites on every pull request, as well as peer code reviews.
</enforcement>