# Fumadocs Library Adoption for Documentation Architecture: Content Loading Metadata Extraction Use Fumadocs

These rules are ALWAYS ACTIVE for all documentation application layout wrappers, page routes, content loading, source indexing, and MDX rendering modules requiring structured content hierarchies.

### Rules

- **R-DOC-001** MUST: Content loading and metadata extraction MUST use `fumadocs-core/source` and `fumadocs-mdx` rather than ad-hoc file-system traversal or custom content parsers.

### Verify

```bash
# Discover and execute the repository dependency audit script to confirm resolved Fumadocs package versions adhere to the lock artifact.
# Discover and run the project typecheck and lint verification tasks to confirm Fumadocs layout imports and source loader interfaces conform to design constraints.
# Discover and execute the workspace test suite to validate that documentation layouts, search components, and MDX loaders render successfully.
```

**Accept when:**
- All documentation and blog page routes resolve navigation and content via Fumadocs UI layouts and Core source loaders without runtime errors.
- Static analysis, type checking, and linting suites pass without unapproved custom documentation layout implementations.
- The project test suite passes with all documentation rendering and search dialog integration tests verified.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks execute typechecking, linting, and build verification, and pull requests bypassing Fumadocs source loaders will fail review gates.
</enforcement>