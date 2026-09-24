# Zod Core Subsystem Modularization: Encapsulating ZodError and Parsing Helper Utilities: Core Validation Architecture Encapsulate Failure State

These rules are ALWAYS ACTIVE for all core validation library modules, schema type implementations, parsing pipelines, and error handling structures.

### Rules

- **R-ZOD-001** MUST: The core validation architecture MUST encapsulate validation failure state inside the dedicated ZodError core subsystem while delegating parsing control flows to specialized parse and safeParse execution handlers.
- **R-ZOD-002** MUST: Ensure all schema type implementations define both throwing and non-throwing parsing methods adhering to the standardized error encapsulation contract.
- **R-ZOD-003** MUST: Maintain strict separation between locale message resolution and schema check evaluators by directing issue generation through centralized error utility modules.

### Verify

```bash
# Discover and execute the repository type-checking script to confirm interface compliance across core schema types and helper modules.
# Discover and run the project test execution suite targeting validation parsing and error formatting behaviors.
```

**Accept when:**
- All core schema types successfully implement parse and safeParse interfaces with zero type-checking diagnostics.
- Test execution suite verifies that validation failures produce correctly formatted ZodError instances without uncaught internal exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests bypassing ZodError encapsulation or directly embedding error formatting in schema types will be blocked until compliant.
</enforcement>