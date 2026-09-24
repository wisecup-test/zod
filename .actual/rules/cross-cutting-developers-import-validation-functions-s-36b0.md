# Valibot Modular Schema Validation Adoption: Developers Import Validation Functions Schema Primitives

These rules are ALWAYS ACTIVE for runtime input parsing, structured schema definition, and payload validation across application modules and performance-sensitive packages.

### Rules

- **R-VAL-001** MUST: Developers MUST import validation functions and schema primitives individually to ensure optimal tree-shaking and dead-code elimination.
- **R-VAL-002** MANDATORY: Execute the Lock-Version Grounding sequence (find manifest, identify build tool, inspect lock/resolution artifact, look up exact version documentation, confirm API existence) before writing code that uses a versioned library.
- **R-VAL-003** MANDATORY: Construct schemas using modular functional composition, importing only the specific validators and types required for each payload.
- **R-VAL-004** MANDATORY: Verify tree-shaking metrics during module bundling to ensure dead-code elimination operates effectively on schema definitions.

### Verify

```bash
# Discover the project test runner from the dependency manifest and execute the test suite
# Discover and run the project build script to confirm that tree-shaking and bundle generation succeed
```

**Accept when:**
- All schema validation tests pass across packages importing the validation library.
- Production bundle analysis confirms that only imported validation primitives are included in target distribution artifacts.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks and peer code reviews enforce modular import practices, and pull requests violating these standards will fail checks and require remediation.
</enforcement>