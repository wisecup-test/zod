# Adopt Event-Driven Integration Pattern for API Boundaries: Event Consumers Idempotent

These rules are ALWAYS ACTIVE for all API integration implementations and boundary definitions within the system, including all new integration points, cross-service communication patterns, and asynchronous operations that span multiple execution contexts.

### Rules

- **R-EVT-001** SHOULD: Event consumers SHOULD be idempotent to handle duplicate message delivery.

### Verify

```bash
# Detect event-driven patterns in API boundary code
grep -r "addEventListener\|EventEmitter\|on(\|emit(" packages/tsc --include="*.ts" | wc -l

# Verify async/await patterns in integration modules
grep -r "async.*await\|Promise<" packages/tsc/bisect.ts packages/tsc/bench/index.ts

# Find event-driven infrastructure definitions
find . -name "*.ts" -exec grep -l "event.*driven\|EventBus\|MessageBroker" {} \;
```

**Accept when:**
- Event-driven patterns are detected in API boundary code with grep commands returning matches in integration modules
- Code review confirms no direct synchronous dependencies between independently deployable components
- Event schema definitions exist with version identifiers and backward compatibility documentation
- Integration tests demonstrate idempotent event handling and proper retry behavior
- Event consumers implement deduplication logic (idempotency tokens, request IDs, or state tracking)
- Cross-boundary API calls use event-driven communication rather than synchronous method invocation

<enforcement>
Claude Code MUST NOT skip or defer verification. All integration points crossing service or module boundaries MUST be reviewed for idempotent event consumer implementation. Violations discovered in code review MUST be flagged and remediated before merge.
</enforcement>