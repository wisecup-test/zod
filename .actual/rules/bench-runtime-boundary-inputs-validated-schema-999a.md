# Zod Schema Validation Adoption: Runtime Boundary Inputs Validated Schema Parse

These rules are ALWAYS ACTIVE for modules defining, validating, or evaluating structured data payloads across execution boundaries, and components processing external or unverified input structures.

### Rules

- **R-ZOD-001** MUST: Runtime boundary inputs MUST be validated using the schema parse method to ensure adherence to the declared schema.
- **R-ZOD-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-ZOD-003** MANDATORY: Before writing code that uses a versioned library, execute the lock-version grounding sequence (find dependency manifest, identify build tool, inspect repository lock/resolution artifact, look up official documentation for that exact version, confirm every API exists, and re-run per dependency at point of use).

### Verify

```bash
# Discover the project verification script from the repository manifest and execute validation
# Discover the project type check configuration and execute static analysis
```

**Accept when:**
- All data structures entering validation boundaries conform to defined zod schemas and pass schema parse calls without error.
- Repository verification scripts execute successfully with zero validation or type checking errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration test suites, static analysis checks, and peer code reviews enforce that untrusted inputs pass through schema parse methods.
</enforcement>