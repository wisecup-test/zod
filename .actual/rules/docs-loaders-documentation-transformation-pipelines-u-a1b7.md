# Remark Middleware Processing Pipeline: Documentation Transformation Pipelines Use Remark Chained

These rules are ALWAYS ACTIVE for documentation loaders and transformation pipelines that parse Markdown and MDX documents into serialized text.

### Rules

- **R-REM-001** MUST: Documentation transformation pipelines MUST use remark with chained middleware plugin attachments via the use method to parse, transform, and serialize content.

### Verify

```bash
# Discover and run the project test runner against documentation loader test suites to verify transformation outputs.
# Discover and execute the project linter and type checker to validate middleware pipeline types and plugin signatures.
```

**Accept when:**
- All documentation loader test suites pass, verifying accurate transformation of MDX and Markdown sources into expected serialized strings.
- Static type checks pass with zero errors across all remark pipeline and plugin invocation sites.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration pipelines, architectural reviews, and static analysis checks.
</enforcement>