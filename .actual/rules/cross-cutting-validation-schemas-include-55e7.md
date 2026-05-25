# Adopt Schema-Based Validation with Benchmarking for Integration Patterns: Validation Schemas Include

These rules are ALWAYS ACTIVE for all integration boundary code including message queue payload validation, API request and response validation, inter-component data transfer validation, external system integration boundaries, and event-driven architecture message validation.

### Rules

- **R-27-001** MAY: Validation schemas MAY include metadata such as descriptions and default values to enhance developer experience and documentation.

### Verify

```bash
# Count schema-based validation patterns across codebase
grep -r "z\.object\|z\.string\|z\.number\|schema" packages/*/src --include="*.ts" | wc -l

# Find benchmark files that include schema or validation logic
find . -name "*benchmark*.ts" -o -name "*bench*.ts" | xargs grep -l "schema\|validation" | wc -l

# Verify message queue boundary associations
grep -r "boundaries\.message_queues" . --include="*.ts" | wc -l
```

**Accept when:**
- Schema validation is present at all identified integration boundaries (message queues, API endpoints)
- Each schema definition has corresponding performance benchmarks measuring validation overhead
- Validation coverage metrics show >90% of integration points have schema-based validation implemented

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated CI checks MUST scan for integration boundary code patterns without corresponding schema validation. Code review MUST enforce schema validation for new integration points. Performance regression testing MUST validate benchmark thresholds in CI pipeline.
</enforcement>