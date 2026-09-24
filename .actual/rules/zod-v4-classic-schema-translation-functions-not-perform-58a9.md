# Zod Contextual Reference Cache and Circular Reference Tracking Pattern: Schema Translation Functions Not Perform Recursive

These rules are ALWAYS ACTIVE for all schema translation and structural conversion code paths dealing with nested, cyclic, or shared reference identifiers.

### Rules

- **R-ZOD-001** MUST_NOT: Schema translation functions MUST NOT perform recursive reference expansion without querying and updating the contextual cache via `ctx.refs.set`.

### Verify

```bash
# Discover and run the project test runner to verify that recursive schema reference tests pass without stack overflow
# Execute the project static analysis and linting suites to ensure context parameters are consistently passed to schema transformation calls
```

**Accept when:**
- All unit tests covering circular and self-referencing schema compilation complete successfully without recursion errors.
- Static type analysis confirms all schema conversion functions conform to expected context signatures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests omitting reference cache checks or cycle tracking cleanup in schema translation modules will be blocked during review.
</enforcement>