# Zod Contextual Reference Cache and Circular Reference Tracking Pattern: Components Converting Schema Representations Isolate Input

These rules are ALWAYS ACTIVE for components converting structural schema specifications into programmatic schema validator objects.

### Rules

- **R-ZOD-001** SHOULD: Components converting schema representations SHOULD isolate input sanitization by parsing deep copies of source definitions prior to reference graph resolution.
- **R-ZOD-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-ZOD-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps per dependency at point of use.
- **R-ZOD-004** MANDATORY: Instantiate a fresh context object containing refs and processing collections at the entry point of each schema conversion routine.
- **R-ZOD-005** MANDATORY: Ensure all downstream schema construction helpers accept and propagate the contextual reference cache.

### Verify

```bash
# Discover and run the project test runner to verify recursive schema reference tests pass without stack overflow
# Execute the project static analysis and linting suites to ensure context parameters are consistently passed to schema transformation calls
```

**Accept when:**
- All unit tests covering circular and self-referencing schema compilation complete successfully without recursion errors.
- Static type analysis confirms all schema conversion functions conform to expected context signatures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>