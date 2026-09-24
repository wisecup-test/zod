# Remark Middleware Processing Pipeline: Remark Processing Pipeline Attach Syntax Specific

These rules are ALWAYS ACTIVE for documentation loaders and transformation pipelines that parse Markdown and MDX documents into serialized text.

### Rules

- **R-REM-001** MUST: The remark processing pipeline MUST attach syntax-specific middleware plugins in sequential order starting with input parsing plugins, proceeding to intermediate transformation plugins, and concluding with serialization via remarkStringify.

### Verify

```bash
# Discover and run the project test runner against documentation loader test suites to verify transformation outputs.
# Discover and execute the project linter and type checker to validate middleware pipeline types and plugin signatures.
```

**Accept when:**
- All documentation loader test suites pass, verifying accurate transformation of MDX and Markdown sources into expected serialized strings.
- Static type checks pass with zero errors across all remark pipeline and plugin invocation sites.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is enforced by automated continuous integration pipeline executing unit and integration tests for document loaders, and architectural/peer code reviews.
</enforcement>