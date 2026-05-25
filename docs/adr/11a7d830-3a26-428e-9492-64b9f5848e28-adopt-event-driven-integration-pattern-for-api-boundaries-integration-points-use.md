# Adopt Event-Driven Integration Pattern for API Boundaries: Integration Points Use

Status: proposed
Date: 2024-01-15
Deciders: Detection Pipeline (automated)

## Activation

This ADR is ACTIVE for all API integration implementations and boundary definitions within the system. All new integration points and API boundaries must comply with the event-driven pattern specified herein.

## Context

- The codebase exhibits a consistent pattern of event-driven architecture at API boundaries, detected across multiple TypeScript modules with 92.50% confidence
- Integration points require decoupling between components to enable independent scaling, testing, and deployment of services
- The bisect and benchmark modules demonstrate the need for asynchronous communication patterns that don't create tight coupling between system components
- Event-driven boundaries provide better fault isolation and enable temporal decoupling between producers and consumers
- The pattern appears in critical infrastructure code (TypeScript compiler tooling), indicating it's a foundational architectural choice

## Problem Statement

Traditional synchronous API integration patterns create tight coupling between components, making systems brittle and difficult to scale. When components communicate through direct method calls or synchronous HTTP requests, failures cascade, deployments become coordinated nightmares, and independent evolution of services becomes impossible. The system needs a standardized approach to API boundaries that enables loose coupling, fault isolation, and independent component lifecycle management.

## Decision

1. MUST: All API integration points MUST use event-driven communication patterns for cross-boundary interactions

## Policy Block

- MUST All API integration points MUST use event-driven communication patterns for cross-boundary interactions

In scope:
- All API endpoints that cross service or module boundaries
- Integration points between independently deployable components
- Communication patterns in TypeScript compiler tooling infrastructure
- Benchmark and bisect operations that trigger cross-component workflows
- Any asynchronous operations that span multiple execution contexts

Out of scope:
- Internal method calls within a single module or bounded context
- Database queries and ORM operations
- File system operations and local I/O
- Synchronous utility functions and pure computations
- UI event handlers that don't cross service boundaries

Exceptions:
- EXC-001: Real-time user-facing operations require sub-100ms latency guarantees that cannot be met with event-driven patterns
- EXC-002: Legacy system integration where the external system only supports synchronous protocols

## Rationale

- Pattern detection identified event-driven boundaries in 2 critical infrastructure files with 92.50% confidence, indicating this is an established architectural principle
- Event-driven integration enables independent scaling of components, as producers and consumers can scale based on their own load characteristics
- Temporal decoupling through events allows components to be deployed, updated, and maintained independently without coordinated releases
- The pattern's presence in TypeScript compiler tooling (bisect and benchmark modules) suggests it's proven effective for complex, performance-critical operations

## Consequences

Positive:
- Components can be developed, tested, and deployed independently, accelerating development velocity
- System resilience improves as failures in one component don't cascade to others through synchronous call chains
- Horizontal scaling becomes simpler as event consumers can be added without modifying producers
- Audit trails and observability improve naturally as events provide a record of system interactions

Negative:
- Increased system complexity due to eventual consistency and asynchronous communication patterns
- Debugging becomes more challenging as request flows span multiple components and time periods
- Infrastructure overhead increases with message brokers, queues, and event storage requirements
- Development teams need additional training on event-driven patterns, idempotency, and distributed system concepts

## Alternatives

- Synchronous REST API calls with circuit breakers (rejected)
  Rejected because: Creates tight coupling between services and doesn't provide temporal decoupling. Circuit breakers mitigate but don't eliminate cascading failures. Prevents independent deployment and scaling.
  When valid: Only valid within bounded contexts where components share lifecycle and deployment cadence
- GraphQL federation with synchronous resolvers (rejected)
  Rejected because: While GraphQL provides schema flexibility, synchronous resolvers still create tight coupling and don't enable temporal decoupling. Doesn't address the core integration boundary concerns.
  When valid: Appropriate for API gateway layer but should delegate to event-driven backends
- Hybrid approach with events for async operations and sync for queries (accepted)
  When valid: Commands use event-driven patterns while queries may use synchronous patterns with appropriate caching and circuit breakers (CQRS-style)

## Risks

- Event schema evolution may break consumers if not managed carefully, causing production incidents
  Mitigation: Implement schema registry with validation, enforce backward compatibility checks in CI/CD, and maintain schema version documentation
  Owner: Platform Engineering Team
- Message ordering guarantees may be lost in distributed event systems, causing data inconsistencies
  Mitigation: Design consumers to be order-independent where possible, use partition keys for ordering requirements, and implement idempotency tokens
  Owner: Engineering Team
- Increased latency from asynchronous patterns may impact user experience for time-sensitive operations
  Mitigation: Implement optimistic UI updates, provide clear feedback on async operations, and use exception process for true real-time requirements
  Owner: Product and Engineering Teams

## Implementation Notes

- Start by identifying all cross-boundary API calls in existing code and prioritize migration based on coupling severity and deployment friction
- Establish event naming conventions (e.g., domain.entity.action) and payload schemas before implementing producers and consumers
- Implement observability infrastructure (distributed tracing, correlation IDs) before migrating critical paths to event-driven patterns
- Create reusable libraries or frameworks for common event patterns (retry logic, dead letter handling, idempotency) to ensure consistency
- For TypeScript projects, leverage type-safe event definitions and consider using tools like Zod or io-ts for runtime schema validation

## Continuation Context


Verify commands:
- grep -r "addEventListener\|EventEmitter\|on(\|emit(" packages/tsc --include="*.ts" | wc -l
- grep -r "async.*await\|Promise<" packages/tsc/bisect.ts packages/tsc/bench/index.ts
- find . -name "*.ts" -exec grep -l "event.*driven\|EventBus\|MessageBroker" {} \;

Accept when:
- Event-driven patterns are detected in API boundary code with grep commands returning matches in integration modules
- Code review confirms no direct synchronous dependencies between independently deployable components
- Event schema definitions exist with version identifiers and backward compatibility documentation
- Integration tests demonstrate idempotent event handling and proper retry behavior

## Enforcement

- Verified by: Automated static analysis in CI/CD pipeline scanning for synchronous cross-boundary calls
- Verified by: Architecture review for new integration points and API boundary definitions
- Verified by: Code review checklist items for event schema versioning and idempotency
- Verified by: Periodic architecture audits using pattern detection tools to identify violations
- Violation handling: CI/CD pipeline fails if static analysis detects synchronous cross-boundary calls without approved exceptions
- Violation handling: Pull requests blocked until architecture review approves integration approach
- Violation handling: Violations discovered in production trigger technical debt tickets with priority based on coupling severity
- Violation handling: Quarterly architecture reviews identify systemic violations for remediation planning
- Exception process: Submit exception request to architecture review board with documented justification and latency/integration requirements
- Exception process: Provide evidence of attempted event-driven solutions and specific technical constraints
- Exception process: Include migration plan or adapter pattern design to isolate synchronous integration
- Exception process: Exceptions reviewed quarterly and must be renewed or remediated