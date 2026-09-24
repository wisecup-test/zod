# Lucide React Adoption for UI Iconography: Visual Icons Graphical Glyphs Rendered Within

These rules are ALWAYS ACTIVE for documentation interface components, content loaders, and metadata schemas requiring visual icons or interactive status glyphs.

### Rules

- **R-LUC-001** MUST: All visual icons and graphical glyphs rendered within documentation interface components and content source loaders MUST be imported and rendered from the adopted lucide-react library.
- **R-LUC-002** MUST: Inspect the repository lock artifact to confirm the active locked version prior to adding new icon references or calling dependency APIs.
- **R-LUC-003** MUST: Mandate accessible label props or screen-reader text on all interactive components rendering icon primitives.

### Verify

```bash
# Discover and run the project static analysis and type-checking scripts
npm run type-check || pnpm type-check || yarn type-check

# Discover and run the project linting and validation suites
npm run lint || pnpm lint || yarn lint

# Discover and run the project automated test suites
npm run test || pnpm test || yarn test
```

**Accept when:**
- All interface icon elements are imported directly from the adopted lucide-react library without unresolved module errors.
- Static analysis and lint checks pass cleanly with no prohibited inline vector elements or unapproved icon dependencies.
- Component test suites pass without accessibility warnings or rendering defects.

<enforcement>
Claude Code MUST NOT skip or defer verification. All visual icons and graphical glyphs rendered within documentation interface components and content source loaders must be verified for compliance with the adopted lucide-react library standards.
</enforcement>