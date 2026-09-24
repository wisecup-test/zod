# fumadocs-ui Layout Adoption for Documentation and Content Presentation: Consumer Inspect Repository Dependency Resolution Artifact

These rules are ALWAYS ACTIVE for route layout modules, shared configuration modules, and documentation or content presentation components.

### Rules

- **R-FUM-001** MUST: The consumer MUST inspect the repository dependency resolution artifact to determine the exact resolved version of the layout library before calling its export interfaces.
- **R-FUM-002** MUST: Derive shared navigation, title, and theme parameters through a unified application layout configuration module to maintain consistency across distinct route layouts.
- **R-FUM-003** MUST: Pass documentation tree sources and navigation loaders to specialized reference documentation layouts while keeping marketing and blog layouts decoupled from documentation source trees.

### Verify

```bash
# Discover and execute the repository type-checking script to verify interface compatibility
# Discover and execute the repository static analysis suite to verify absence of disallowed custom layout wrappers
# Discover and execute the repository build script to confirm successful compilation of all route layout boundaries
```

**Accept when:**
- Documentation route layouts successfully render navigation, sidebars, and body content using fumadocs-ui layout components without layout structural errors.
- All layout components resolve their configuration and source definitions through the standardized shared application configuration contract.
- The repository static verification suite passes without module resolution or layout contract violations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, type-checking, and build verification must confirm layout property contracts and module imports.
</enforcement>