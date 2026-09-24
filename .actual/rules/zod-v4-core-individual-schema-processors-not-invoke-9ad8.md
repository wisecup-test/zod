# json-schema-processors Internal Module Adoption for Schema Transformation: Individual Schema Processors Not Invoke Sibling

These rules are ALWAYS ACTIVE for internal modules implementing schema-to-schema transformation within the core library, including processors and generators handling schema serialization and validation keyword mapping.

### Rules

- **R-JSON-001** MUST_NOT: Individual schema processors MUST NOT invoke sibling processors directly; nested and referenced schema conversions MUST be delegated through the central schema transformation dispatcher.

### Verify

```bash
# Discover the project test runner script from the root package manifest and execute the core test suite covering schema transformation.
# Inspect the build configuration to identify and run the type-checking and linting verification tasks across core modules.
```

**Accept when:**
- All unit tests covering schema transformation processors and generator pipelines execute successfully without regression.
- Cyclic schema references resolve to valid references without triggering call stack exceptions.
- Static type analysis and module linting checks pass with zero reported errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline executes unit tests and static analysis. Mandatory peer code review for changes affecting core schema transformation modules. Pull requests bypassing the processor architecture or omitting context cache lookups will fail automated checks and be blocked from merging.
</enforcement>