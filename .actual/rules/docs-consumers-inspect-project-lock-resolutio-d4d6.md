# fumadocs-core Source Loader Integration: Consumers Inspect Project Lock Resolution Artifact

These rules are ALWAYS ACTIVE for documentation workspace modules responsible for loading, indexing, or traversing page content, as well as route handlers and loader utilities that serialize documentation pages for downstream consumers.

### Rules

- **R-FUM-001** MUST: Consumers MUST inspect the project lock and resolution artifact to resolve the exact installed version of fumadocs-core before consuming or altering source loader interfaces, ensuring API compatibility with the active environment.

### Verify

```bash
# Discover workspace root configuration to locate the documentation test execution task, then execute the test suite
# Identify project type check script in the package manifest and run type checker across documentation modules
# Locate and execute documentation build validation script
```

**Accept when:**
- All source loader consumers and route handlers compile without type errors against the resolved source module definitions.
- Documentation endpoints successfully traverse the page hierarchy and serialize page content through the centralized source loader interface.
- Test suites validating documentation content extraction and page ordering pass with zero regressions.

<enforcement>
Claude Code MUST NOT skip or defer verification. All modifications to documentation loader interfaces and route handlers are verified by automated static analysis, type checking, and peer code reviews.
</enforcement>