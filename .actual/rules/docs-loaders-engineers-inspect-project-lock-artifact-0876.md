# Remark Middleware Processing Pipeline: Engineers Inspect Project Lock Artifact Resolve

These rules are ALWAYS ACTIVE for documentation loaders and transformation pipelines that parse Markdown and MDX documents into serialized text.

### Rules

- **R-REM-001** MUST: Engineers MUST inspect the project lock artifact and resolve the exact locked version of remark and its associated plugins before implementing pipeline extensions.

### Verify

```bash
# Discover and execute the project test runner against documentation loader test suites
# Discover and execute the project linter and type checker to validate middleware pipeline types and plugin signatures
```

**Accept when:**
- All documentation loader test suites pass, verifying accurate transformation of MDX and Markdown sources into expected serialized strings.
- Static type checks pass with zero errors across all remark pipeline and plugin invocation sites.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification of documentation loader test suites and static type checks is mandatory.
</enforcement>