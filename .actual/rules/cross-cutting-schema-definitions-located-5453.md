# Adopt Schema-Based Validation with Benchmarking for Integration Patterns: Schema Definitions Located

These rules are ALWAYS ACTIVE for all integration boundary code, message queue handlers, API endpoints, and inter-component data transfer validation points.

### Rules

- **R-27-001** SHOULD: Schema definitions SHOULD be co-located with their corresponding benchmark tests to facilitate performance regression detection.
- **R-27-002** MUST: Mandatory benchmarking ensures validation performance is monitored and overhead is tracked continuously.

### Verify

```bash
# Count schema validation patterns across codebase
grep -r "z\.object\|z\.string\|z\.number\|schema" packages/*/src --include="*.ts" | wc -l

# Find benchmark files with schema/validation references
find . -name "*benchmark*.ts" -o -name "*bench*.ts" | xargs grep -l "schema\|validation" | wc -l

# Verify message queue boundary validation patterns
grep -r "boundaries\.message_queues" . --include="*.ts" | wc -l
```

**Accept when:**
- Schema validation is present at all identified integration boundaries (message queues, API endpoints, inter-component communication)
- Each schema definition has corresponding performance benchmarks measuring validation overhead
- Validation coverage metrics show >90% of integration points have schema-based validation implemented
- Benchmark tests are co-located with schema definitions in the same directory or module

<enforcement>
Claude Code MUST NOT skip or defer verification. All integration boundaries identified in the codebase MUST have corresponding schema definitions with benchmarks, or documented exceptions (EXC-001 for performance-critical hot paths, EXC-002 for legacy integration points under migration) must be present and tracked.
</enforcement>