# fumadocs-core Source Loader Integration: Documentation Content Ingestion Page Tree Traversal

These rules are ALWAYS ACTIVE for all documentation workspace modules responsible for loading, indexing, or traversing page content, as well as route handlers and loader utilities that serialize documentation pages for downstream consumers.

### Rules

- **R-DOC-001** MUST: All documentation content ingestion and page tree traversal within the documentation workspace MUST standardize on the fumadocs-core/source module as the authoritative content source interface rather than implementing bespoke filesystem parsing routines.

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
Claude Code MUST NOT skip or defer verification. Automated static analysis, type checking, and peer code reviews enforce compliance.
</enforcement>