# Schema Optionality Unification and Absent Key Semantics: Object Property Validation Tuple Element Handling

These rules are ALWAYS ACTIVE for core schema definitions, classic schema definitions, and composite wrapper schemas including preprocess, catch, tuple, and optionality handling.

### Rules

- **R-SCH-001** SHOULD: Object property validation and tuple element handling SHOULD adhere to the unified opt-in and opt-out propagation rules specified in wiki/optionality.md.

### Verify

```bash
# Discover and run the project's test suite for schema validation, catch, preprocess, and tuple optionality
npm test
```

**Accept when:**
- Inner schema fallbacks and transforms execute when wrapper schemas receive absent keys or undefined inputs.
- All test cases covering catch, preprocess, partial, tuple, and optional schemas pass without regressions.
- Schema behavior aligns with missing-key resolution specifications in wiki/optionality.md.

<enforcement>
Verification is mandatory. Claude Code MUST NOT skip or defer verification. Automated CI test failures and pull request reviews enforce adherence to wiki/optionality.md.
</enforcement>