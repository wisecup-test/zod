# Remark Middleware Processing Pipeline: Custom String Transformations Regular Expressions Not

These rules are ALWAYS ACTIVE for documentation loaders and transformation pipelines that parse Markdown and MDX documents into serialized text.

### Rules

- **R-RMK-001** MUST_NOT: Custom string transformations and regular expressions MUST_NOT be used to parse or modify document abstract syntax trees outside of the remark plugin lifecycle.

### Verify

```bash
# Discover and run the project test runner against documentation loader test suites to verify transformation outputs.
# Discover and execute the project linter and type checker to validate middleware pipeline types and plugin signatures.
```

**Accept when:**
- All documentation loader test suites pass, verifying accurate transformation of MDX and Markdown sources into expected serialized strings.
- Static type checks pass with zero errors across all remark pipeline and plugin invocation sites.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>