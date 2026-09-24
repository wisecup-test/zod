# Zod Core Subsystem Modularization: Encapsulating ZodError and Parsing Helper Utilities: Localization Mappings Default Error Message Generators

These rules are ALWAYS ACTIVE for all core schema validation modules, parsing pipelines, and error handling structures.

### Rules

- **R-ZOD-001** SHOULD: Localization mappings and default error message generators SHOULD be encapsulated in independent locale modules decoupled from schema validation check evaluators.
- **R-ZOD-002** MANDATORY: All schema type implementations MUST define both throwing (`parse`) and non-throwing (`safeParse`) parsing methods adhering to the standardized error encapsulation contract.
- **R-ZOD-003** MANDATORY: Maintain strict separation between locale message resolution and schema check evaluators by directing issue generation through centralized error utility modules.

### Verify

```bash
# Discover and execute the repository type-checking script to confirm interface compliance across core schema types and helper modules.
# Discover and run the project test execution suite targeting validation parsing and error formatting behaviors.
```

**Accept when:**
- All core schema types successfully implement parse and safeParse interfaces with zero type-checking diagnostics.
- Test execution suite verifies that validation failures produce correctly formatted ZodError instances without uncaught internal exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipelines and peer code reviews enforce ZodError encapsulation across all core modules.
</enforcement>