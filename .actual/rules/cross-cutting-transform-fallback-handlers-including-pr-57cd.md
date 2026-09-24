# Schema Optionality Unification and Absent Key Semantics: Transform Fallback Handlers Including Preprocess Catch

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-OPT-001** MUST: Transform and fallback handlers, including z.preprocess, catch, and default configurations, MUST evaluate within the inner schema context before outer optionality resolution short-circuits execution.

### Verify

```bash
# Discover and run the project's test suite for schema validation, catch, preprocess, and tuple optionality.
npm test
```

**Accept when:**
- Inner schema fallbacks and transforms execute when wrapper schemas receive absent keys or undefined inputs.
- All test cases covering catch, preprocess, partial, tuple, and optional schemas pass without regressions.
- Schema behavior aligns with missing-key resolution specifications in wiki/optionality.md.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration schema test suites and architectural peer review verify compliance.
</enforcement>