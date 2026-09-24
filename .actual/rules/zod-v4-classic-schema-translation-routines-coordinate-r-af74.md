# Zod Contextual Reference Cache and Circular Reference Tracking Pattern: Schema Translation Routines Coordinate Reference Resolution

These rules are ALWAYS ACTIVE for schema translation routines and conversion processes involving structural schema specifications, shared reference identifiers, and potential circular dependencies.

### Rules

- **R-ZOD-001** MUST: Schema translation routines MUST coordinate reference resolution through a shared context object providing memoized lookup via ctx.refs and cycle tracking via ctx.processing.

### Verify

```bash
# Discover and run the project test runner to verify that recursive schema reference tests pass without stack overflow.
# Execute the project static analysis and linting suites to ensure context parameters are consistently passed to schema transformation calls.
```

**Accept when:**
- All unit tests covering circular and self-referencing schema compilation complete successfully without recursion errors.
- Static type analysis confirms all schema conversion functions conform to expected context signatures.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests omitting reference cache checks or cycle tracking cleanup in schema translation modules will be blocked during review, and static verification failures on context interface mismatches halt compilation.
</enforcement>