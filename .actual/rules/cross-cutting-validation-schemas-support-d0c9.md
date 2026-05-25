# Adopt Schema-Based Validation with Benchmarking for Integration Patterns: Validation Schemas Support

These rules are ALWAYS ACTIVE for all integration boundary code including message queue handlers, API endpoints, inter-component data transfer, and external system integration points.

### Rules

- **R-27-001** MUST: Validation schemas MUST support common data types including primitives, objects, unions, discriminated unions, and complex nested structures.
- **R-27-002** MUST: Each schema definition MUST have corresponding performance benchmarks measuring validation overhead.
- **R-27-003** MUST: Schema validation MUST be present at all identified integration boundaries (message queues, API endpoints, inter-component communication).
- **R-27-004** SHOULD: Establish baseline performance benchmarks before implementing validation to measure actual overhead.
- **R-27-005** SHOULD: Create reusable schema libraries for common patterns (datetime, IP addresses, standard objects) to reduce duplication.
- **R-27-006** SHOULD: Integrate validation failures into observability infrastructure for monitoring and alerting.
- **R-27-007** MAY: Provide exception process for performance-critical hot paths where validation overhead exceeds 5% of total execution time (EXC-001).
- **R-27-008** MAY: Allow legacy integration points undergoing gradual migration to defer full schema validation compliance (EXC-002).

### Verify

```bash
# Count schema validation usage across codebase
grep -r "z\.object\|z\.string\|z\.number\|schema" packages/*/src --include="*.ts" | wc -l

# Find benchmark files with schema/validation references
find . -name "*benchmark*.ts" -o -name "*bench*.ts" | xargs grep -l "schema\|validation" | wc -l

# Verify message queue boundary associations
grep -r "boundaries\.message_queues" . --include="*.ts" | wc -l
```

**Accept when:**
- Schema validation is present at all identified integration boundaries (message queues, API endpoints)
- Each schema definition has corresponding performance benchmarks measuring validation overhead
- Validation coverage metrics show >90% of integration points have schema-based validation implemented
- Validation failures are integrated into observability infrastructure with monitoring and alerting
- Performance regression testing in CI pipeline validates benchmark thresholds

<enforcement>
Claude Code MUST NOT skip or defer verification. All integration boundary code MUST be checked for schema validation presence and performance benchmarks. CI pipeline MUST fail if new integration boundaries lack schema validation without documented exception. Code review MUST block merge if validation requirements not met.
</enforcement>