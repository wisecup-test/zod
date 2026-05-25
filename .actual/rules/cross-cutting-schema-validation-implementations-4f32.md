# Adopt Schema-Based Validation with Benchmarking for Integration Patterns: Schema Validation Implementations

These rules are ALWAYS ACTIVE for all integration boundary code including message queue payload validation, API request and response validation, inter-component data transfer validation, external system integration boundaries, and event-driven architecture message validation.

### Rules

- **R-27-002** MUST: Schema validation implementations MUST include performance benchmarks to ensure validation overhead remains within acceptable thresholds.

### Verify

```bash
# Count schema validation patterns in codebase
grep -r "z\.object\|z\.string\|z\.number\|schema" packages/*/src --include="*.ts" | wc -l

# Find benchmark files with schema/validation references
find . -name "*benchmark*.ts" -o -name "*bench*.ts" | xargs grep -l "schema\|validation" | wc -l

# Verify message queue boundary patterns
grep -r "boundaries\.message_queues" . --include="*.ts" | wc -l
```

**Accept when:**
- Schema validation is present at all identified integration boundaries (message queues, API endpoints)
- Each schema definition has corresponding performance benchmarks measuring validation overhead
- Validation coverage metrics show >90% of integration points have schema-based validation implemented

<enforcement>
Claude Code MUST NOT skip or defer verification. All integration boundaries identified in the codebase must have corresponding schema validation with performance benchmarks before code review approval.
</enforcement>