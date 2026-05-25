# Adopt Event-Driven Integration Pattern for API Boundaries: Dead Letter Queues

These rules are ALWAYS ACTIVE for all API integration implementations and boundary definitions within the system, including all new integration points, cross-service communication patterns, and asynchronous operations that span multiple execution contexts.

### Rules

- **R-DLQ-001** SHOULD: Dead letter queues SHOULD be configured for events that cannot be processed after retry attempts.

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
- Dead letter queue configuration is present for failed event processing with documented retry policies

<enforcement>
Claude Code MUST NOT skip or defer verification. All API boundary implementations MUST be reviewed against these rules before merge. Violations detected by static analysis in CI/CD MUST block pull requests until remediated or approved exceptions are documented.
</enforcement>