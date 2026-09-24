# Zod Contextual Reference Cache and Circular Reference Tracking Pattern: Before Implementing Dependencies Involving Schema Parsing

These rules are ALWAYS ACTIVE for all schema parsing, translation, and reference-resolution code involving schema validation libraries.

### Rules

- **R-ZOD-001** MUST: Before implementing dependencies involving schema parsing or validation libraries, the consumer MUST inspect the repository lock artifact to determine the authoritative resolved version.
- **R-ZOD-002** MUST: Instantiate a fresh context object containing refs and processing collections at the entry point of each schema conversion routine.
- **R-ZOD-003** MUST: Ensure all downstream schema construction helpers accept and propagate the contextual reference cache.

### Verify

```bash
# Discover and run the project test runner to verify that recursive schema reference tests pass without stack overflow
# Execute the project static analysis and linting suites to ensure context parameters are consistently passed to schema transformation calls
```

**Accept when:**
- All unit tests covering circular and self-referencing schema compilation complete successfully without recursion errors.
- Static type analysis confirms all schema conversion functions conform to expected context signatures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests omitting reference cache checks or cycle tracking cleanup in schema translation modules will be blocked during review, and static verification failures on context interface mismatches halt compilation.
</enforcement>