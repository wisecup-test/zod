# fumadocs-core Source Loader Integration: Documentation Consumers Content Generation Endpoints Access

These rules are ALWAYS ACTIVE for all documentation workspace modules, route handlers, and loader utilities responsible for loading, indexing, or traversing page content.

### Rules

- **R-SRC-001** MUST: Documentation consumers and content generation endpoints MUST access pages, page trees, and collection metadata exclusively through the centralized source loader abstractions exported from the content source integration layer.

### Verify

```bash
# Discover the workspace root configuration to locate the documentation test execution task, then execute the suite to verify source loader compatibility.
# Identify the project type check script in the package manifest and run the type checker across documentation modules to validate source loader call signatures.
# Locate and execute the documentation build validation script to ensure route handlers correctly resolve and serialize pages via the source loader.
```

**Accept when:**
- All source loader consumers and route handlers compile without type errors against the resolved source module definitions.
- Documentation endpoints successfully traverse the page hierarchy and serialize page content through the centralized source loader interface.
- Test suites validating documentation content extraction and page ordering pass with zero regressions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests introducing direct filesystem parsing or bypassing the central source loader must be blocked until refactored to use the standardized source interface.
</enforcement>