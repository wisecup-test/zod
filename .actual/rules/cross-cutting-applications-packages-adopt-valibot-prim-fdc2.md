# Valibot Modular Schema Validation Adoption: Applications Packages Adopt Valibot Primary Schema

These rules are ALWAYS ACTIVE for all applications and packages adopting Valibot as the primary schema definition and runtime validation library.

### Rules

- **R-VAL-001** MUST: Applications and packages MUST adopt Valibot as the primary schema definition and runtime validation library for modular payload validation.
- **R-VAL-002** MUST: Construct schemas using modular functional composition, importing only the specific validators and types required for each payload.
- **R-VAL-003** MUST: Follow the MANDATORY Discovery Policy and Lock-Version Grounding instructions before writing code that uses a versioned library.
- **R-VAL-004** MUST: Verify tree-shaking metrics during module bundling to ensure dead-code elimination operates effectively on schema definitions.

### Verify

```bash
# Discover the project test runner from the dependency manifest and execute the test suite
# Discover and run the project build script to confirm tree-shaking and bundle generation succeed
```

**Accept when:**
- All schema validation tests pass across packages importing the validation library.
- Production bundle analysis confirms that only imported validation primitives are included in target distribution artifacts.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks and peer code reviews verify modular import practices and schema boundary definitions.
</enforcement>