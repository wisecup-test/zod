# Standard Schema Specification Module Adoption: Schema Transformation Export Modules Consume Canonical

These rules are ALWAYS ACTIVE for core library modules responsible for schema transformations, schema serialization, validation metadata export, and core error handling and diagnostic reporting.

### Rules

- **R-MOD-001** MUST: Schema transformation and export modules MUST consume the canonical schema registry and core schema definitions alongside the Standard Schema module to preserve metadata fidelity.

### Verify

```bash
# Discover the repository build and type verification script and run it
# Discover the automated test suite execution script from the repository manifest and execute tests
```

**Accept when:**
- All core module static type checks and contract interface verifications pass without compilation or diagnostic errors.
- All automated test suites exercising schema transformation, error construction, and specification interoperability pass successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipelines, static type analysis, and peer code reviews.
</enforcement>