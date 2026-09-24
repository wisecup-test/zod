# Zod Core Subsystem Modularization: Encapsulating ZodError and Parsing Helper Utilities: Schema Type Definitions Not Construct Raw

These rules are ALWAYS ACTIVE for all core validation library modules responsible for defining schema types, parsing pipelines, and error handling structures.

### Rules

- **R-ZOD-001** MUST: Schema type definitions MUST NOT construct raw validation errors directly and MUST route all validation issue construction through dedicated error utility helpers and localized message formatting modules.

### Verify

```bash
# Discover and execute the repository type-checking script to confirm interface compliance across core schema types and helper modules.
# Discover and run the project test execution suite targeting validation parsing and error formatting behaviors.
```

**Accept when:**
- All core schema types successfully implement parse and safeParse interfaces with zero type-checking diagnostics.
- Test execution suite verifies that validation failures produce correctly formatted ZodError instances without uncaught internal exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipelines and peer code reviews enforce compliance.
</enforcement>