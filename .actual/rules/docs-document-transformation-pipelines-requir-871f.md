# fumadocs-core Source Loader Integration: Document Transformation Pipelines Requiring Ast Manipulation

These rules are ALWAYS ACTIVE for documentation workspace modules responsible for loading, indexing, or traversing page content, and route handlers and loader utilities that serialize documentation pages for downstream consumers.

### Rules

- **R-FUM-001** SHOULD: Document transformation pipelines requiring AST manipulation for external consumers compose middleware plugins directly against the loaded source AST representation prior to serialization.

### Verify

```bash
# Discover the workspace root configuration to locate the documentation test execution task, then execute the suite to verify source loader compatibility.
npm test --workspace=docs

# Identify the project type check script in the package manifest and run the type checker across documentation modules to validate source loader call signatures.
npm run typecheck --workspace=docs

# Locate and execute the documentation build validation script to ensure route handlers correctly resolve and serialize pages via the source loader.
npm run build --workspace=docs
```

**Accept when:**
- All source loader consumers and route handlers compile without type errors against the resolved source module definitions.
- Documentation endpoints successfully traverse the page hierarchy and serialize page content through the centralized source loader interface.
- Test suites validating documentation content extraction and page ordering pass with zero regressions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation of these rules (such as introducing direct filesystem parsing or bypassing the central source loader) must be blocked until refactored.
</enforcement>