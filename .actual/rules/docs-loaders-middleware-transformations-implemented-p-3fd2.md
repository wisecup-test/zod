# Remark Middleware Processing Pipeline: Middleware Transformations Implemented Pure Abstract Syntax

These rules are ALWAYS ACTIVE for documentation loaders and transformation pipelines that parse Markdown and MDX documents into serialized text.

### Rules

- **R-RMK-001** SHOULD: Middleware transformations SHOULD be implemented as pure abstract syntax tree visitor plugins to ensure deterministic serialization.
- **R-RMK-002** MANDATORY: Discover the dependency manifest in the repo to derive tool names, file names, commands, package managers, and version numbers.
- **R-RMK-003** MANDATORY: Before writing code that uses a versioned library, inspect the repository lock or resolution artifact to determine the exact resolved version, look up official documentation for that exact version, and confirm every API, class, or function exists in that version.
- **R-RMK-004** MANDATORY: Construct the remark pipeline by chaining use calls, ensuring input parsers precede intermediate AST transforms and stringify serializers.
- **R-RMK-005** MANDATORY: Verify that all plugins registered in the pipeline adhere to the unified syntax tree specification supported by the configured remark version.

### Verify

```bash
# Discover and run the project test runner against documentation loader test suites to verify transformation outputs
# Discover and execute the project linter and type checker to validate middleware pipeline types and plugin signatures
```

**Accept when:**
- All documentation loader test suites pass, verifying accurate transformation of MDX and Markdown sources into expected serialized strings.
- Static type checks pass with zero errors across all remark pipeline and plugin invocation sites.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline executing unit and integration tests for document loaders, and architectural and peer code reviews.
</enforcement>