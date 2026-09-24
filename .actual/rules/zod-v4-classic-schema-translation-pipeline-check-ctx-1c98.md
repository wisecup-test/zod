# Zod Contextual Reference Cache and Circular Reference Tracking Pattern: Schema Translation Pipeline Check Ctx Refs

These rules are ALWAYS ACTIVE for schema translation pipelines handling external structural schema specifications and reference resolution.

### Rules

- **R-ZOD-001** MUST: The schema translation pipeline MUST check ctx.refs using ctx.refs.get before compiling any referenced schema path to avoid redundant instance instantiation.

### Verify

```bash
# Discover and run the project test runner to verify that recursive schema reference tests pass without stack overflow.
# Execute the project static analysis and linting suites to ensure context parameters are consistently passed to schema transformation calls.
```

**Accept when:**
- All unit tests covering circular and self-referencing schema compilation complete successfully without recursion errors.
- Static type analysis confirms all schema conversion functions conform to expected context signatures.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>