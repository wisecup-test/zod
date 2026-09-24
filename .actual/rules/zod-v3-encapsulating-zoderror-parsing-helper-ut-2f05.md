# Zod Core Subsystem Modularization: Encapsulating ZodError and Parsing Helper Utilities: Core Schema Types Implement Both Parse

These rules are ALWAYS ACTIVE for all core schema validation modules, parsing pipelines, and error handling structures.

### Rules

- **R-ZOD-001** MUST: Core schema types MUST implement both parse and safeParse public interfaces where safeParse returns structured result objects encapsulating either successful data or a ZodError instance without throwing uncaught exceptions.
- **R-ZOD-002** MUST: Maintain strict separation between locale message resolution and schema check evaluators by directing issue generation through centralized error utility modules.

### Verify

```bash
# Discover and execute the repository type-checking script to confirm interface compliance across core schema types and helper modules.
# Discover and run the project test execution suite targeting validation parsing and error formatting behaviors.
```

**Accept when:**
- All core schema types successfully implement parse and safeParse interfaces with zero type-checking diagnostics.
- Test execution suite verifies that validation failures produce correctly formatted ZodError instances without uncaught internal exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipelines and peer code reviews enforce these rules, and pull requests bypassing ZodError encapsulation or directly embedding error formatting in schema types will be blocked.
</enforcement>