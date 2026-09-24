# Schema Optionality Unification and Absent Key Semantics: Composite Schemas Wrapping Inner Types Defer

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-COMPOSITE-001** MUST: Composite schemas wrapping inner types MUST defer absent-key and missing-element resolution down to the inner schemas instead of short-circuiting on undefined or absent input.

### Verify

```bash
npx jest packages/zod/src/v4/classic/tests/catch.test.ts packages/zod/src/v4/classic/tests/preprocess.test.ts packages/zod/src/v4/classic/tests/partial.test.ts packages/zod/src/v4/classic/tests/tuple.test.ts packages/zod/src/v4/classic/tests/optional.test.ts
```

**Accept when:**
- Inner schema fallbacks and transforms execute when wrapper schemas receive absent keys or undefined inputs.
- All test cases covering catch, preprocess, partial, tuple, and optional schemas pass without regressions.
- Schema behavior aligns with missing-key resolution specifications in wiki/optionality.md.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling includes automated CI test failures and pull request review rejection for implementations deviating from wiki/optionality.md.
</enforcement>