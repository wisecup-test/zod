# Zod Core Subsystem Modularization: Encapsulating ZodError and Parsing Helper Utilities: Engineers Discover Ecosystem Lock Artifact Within

These rules are ALWAYS ACTIVE for all core schema validation modules, parsing pipelines, and error handling structures within the repository.

### Rules

- **R-ZOD-001** MUST: Engineers MUST discover the ecosystem lock artifact within the repository and verify the exact resolved version of all validation library dependencies prior to introducing or modifying core module abstractions.
- **R-ZOD-002** MUST: All schema type implementations MUST define both throwing and non-throwing parsing methods adhering to the standardized error encapsulation contract.
- **R-ZOD-003** MUST: Maintain strict separation between locale message resolution and schema check evaluators by directing issue generation through centralized error utility modules.

### Verify

```bash
# Discover and execute the repository type-checking script to confirm interface compliance
# Discover and run the project test execution suite targeting validation parsing and error formatting behaviors
```

**Accept when:**
- All core schema types successfully implement parse and safeParse interfaces with zero type-checking diagnostics.
- Test execution suite verifies that validation failures produce correctly formatted ZodError instances without uncaught internal exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated CI pipelines, peer code reviews, and architectural validation enforce these rules.
</enforcement>