# json-schema-processors Internal Module Adoption for Schema Transformation: Schema Generation Orchestration Modules Not Contain

These rules are ALWAYS ACTIVE for internal modules implementing schema-to-schema transformation within the core library, including processors and generators handling schema serialization and validation keyword mapping.

### Rules

- **R-JSON-001** SHOULD_NOT: Schema generation orchestration modules SHOULD NOT contain inline type-specific transformation branches and MUST rely on registered processors.

### Verify

```bash
# Discover and run the project test runner script covering schema transformation
# Inspect the build configuration and run type-checking/linting verification tasks across core modules
npm test
npm run lint
npm run typecheck
```

**Accept when:**
- All unit tests covering schema transformation processors and generator pipelines execute successfully without regression.
- Cyclic schema references resolve to valid references without triggering call stack exceptions.
- Static type analysis and module linting checks pass with zero reported errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline executes unit tests and static analysis, and peer code reviews enforce compliance.
</enforcement>