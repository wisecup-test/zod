# Adopt Event-Driven Integration Pattern for API Boundaries: Integration Points Use

These rules are ALWAYS ACTIVE for all API integration implementations and boundary definitions within the system. All new integration points and API boundaries must comply with the event-driven pattern specified herein.

### Rules

- **R-API-001** MUST: All API integration points MUST use event-driven communication patterns for cross-boundary interactions.

### Verify

```bash
# Detect event-driven patterns in integration modules
grep -r "addEventListener\|EventEmitter\|on(\|emit(" packages/tsc --include="*.ts" | wc -l

# Verify async/await patterns in critical integration files
grep -r "async.*await\|Promise<" packages/tsc/bisect.ts packages/tsc/bench/index.ts

# Find event-driven infrastructure definitions
find . -name "*.ts" -exec grep -l "event.*driven\|EventBus\|MessageBroker" {} \;

# Scan for synchronous cross-boundary calls (violations)
grep -r "import.*from.*\.\." packages/tsc --include="*.ts" | grep -v "EventEmitter\|EventBus" | head -20
```

**Accept when:**
- Event-driven patterns are detected in API boundary code with grep commands returning matches in integration modules
- Code review confirms no direct synchronous dependencies between independently deployable components
- Event schema definitions exist with version identifiers and backward compatibility documentation
- Integration tests demonstrate idempotent event handling and proper retry behavior
- All cross-boundary API calls use asynchronous event-driven communication or approved exceptions

<enforcement>
Claude Code MUST NOT skip or defer verification. Static analysis in CI/CD pipeline MUST scan for synchronous cross-boundary calls. Architecture review MUST approve all integration points. Pull requests MUST be blocked until event-driven compliance is confirmed or exception is granted.
</enforcement>