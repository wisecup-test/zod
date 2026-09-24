# Standard Schema Specification Module Adoption: Developers Discover Ecosystem Lock Resolution Artifact

These rules are ALWAYS ACTIVE for core library modules responsible for schema transformations, schema serialization, validation metadata export, and core error handling.

### Rules

- **R-STD-001** MUST: Developers MUST discover the ecosystem lock resolution artifact and verify the exact resolved version of all external specification and library dependencies before implementation.

### Verify

```bash
# Discover and run the repository build and type verification script
# Discover and execute the automated test suite execution script from the repository manifest
```

**Accept when:**
- All core module static type checks and contract interface verifications pass without compilation or diagnostic errors.
- All automated test suites exercising schema transformation, error construction, and specification interoperability pass successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated CI pipelines and peer code reviews.
</enforcement>