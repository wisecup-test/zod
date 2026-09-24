# Fumadocs Library Adoption for Documentation Architecture: Documentation Layouts Use Fumadocs Docs Page

These rules are ALWAYS ACTIVE for documentation application layout wrappers, page routes, content loading, source indexing, MDX rendering modules, search overlay dialogs, and navigation components within the documentation workspace.

### Rules

- **R-FUMA-001** MUST: Documentation layouts MUST use `fumadocs-ui/layouts/docs` for documentation page hierarchies and `fumadocs-ui/layouts/home` for index and landing views to maintain uniform navigation structures.

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
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks executing typechecking, linting, and build verification, alongside architectural peer review, are mandatory.
</enforcement>