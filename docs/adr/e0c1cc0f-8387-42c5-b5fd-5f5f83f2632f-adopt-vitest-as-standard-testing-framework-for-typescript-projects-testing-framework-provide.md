# Adopt Vitest as Standard Testing Framework for TypeScript Projects: Testing Framework Provide

Status: proposed
Date: 2024-01-09
Deciders: Detection Pipeline (automated)

## Context

- The codebase contains 57 test files following a consistent pattern with .test.ts extensions, indicating a standardized testing approach across multiple package versions (v3, v4/classic, v4/mini, v4/core)
- Test files cover diverse scenarios including async operations, refinements, error handling, localization, codecs, and standard schema compliance, demonstrating comprehensive test coverage requirements
- The pattern shows consistent test organization within package-specific test directories, suggesting a modular testing strategy aligned with package boundaries
- Evidence indicates testing of both synchronous and asynchronous validation patterns, error utilities, and framework-specific features like lazy evaluation and method detachment
- The high confidence (93.08%) and support count (57 files) suggest this is an established, mature testing pattern rather than an experimental approach

## Problem Statement

TypeScript projects require a fast, modern testing framework that supports ESM modules, TypeScript natively, async/await patterns, and provides excellent developer experience with minimal configuration. Traditional testing frameworks like Jest require additional transformation layers and configuration overhead for TypeScript projects, while the codebase needs consistent testing patterns across multiple package versions and test scenarios.

## Decision

1. SHOULD: Testing framework SHOULD provide fast execution times suitable for watch mode during development

## Policy Block

- SHOULD Testing framework SHOULD provide fast execution times suitable for watch mode during development

In scope:
- All TypeScript packages within the monorepo
- Unit tests for validation logic, schemas, and utilities
- Integration tests for async operations and refinements
- Localization and internationalization test suites
- Standard schema compliance tests

Out of scope:
- End-to-end browser tests (may require different tooling)
- Performance benchmarking tests (may use specialized tools)
- Visual regression tests
- Load and stress testing

Exceptions:
- EXC-001: Legacy packages being migrated may temporarily use Jest until migration is complete
- EXC-002: Specialized testing scenarios requiring framework-specific features not available in Vitest

## Rationale

- Pattern detected across 57 test files with 93.08% confidence indicates this is a proven, stable testing approach that has been successfully applied across multiple package versions
- Consistent .test.ts naming convention and tests/ directory structure provides predictable test discovery and organization, reducing cognitive load for developers
- Native TypeScript support eliminates transformation overhead and configuration complexity, improving developer experience and reducing maintenance burden
- Coverage of diverse test scenarios (async, error handling, localization, codecs) demonstrates the framework's versatility and suitability for complex validation library requirements

## Consequences

Positive:
- Fast test execution with native ESM and TypeScript support improves developer productivity and enables efficient watch mode during development
- Consistent test file naming and organization across packages reduces onboarding time and makes test discovery intuitive
- Minimal configuration overhead reduces maintenance burden and allows developers to focus on writing tests rather than configuring tooling
- Strong async/await support aligns with modern JavaScript patterns and simplifies testing of asynchronous validation logic

Negative:
- Teams familiar with Jest may face a learning curve when adopting Vitest, though the API similarity mitigates this
- Some Jest-specific plugins or extensions may not have direct Vitest equivalents, requiring alternative solutions
- Ecosystem maturity is lower than Jest, potentially leading to fewer community resources and third-party integrations
- Migration effort required for any existing Jest-based tests in the codebase

## Alternatives

- Continue using Jest with ts-jest transformer (rejected)
  Rejected because: Requires additional transformation layer, slower execution, more complex configuration, and doesn't align with the detected pattern of native TypeScript testing
  When valid: For projects with extensive Jest-specific tooling investments or when team expertise is exclusively Jest-focused
- Adopt Node.js native test runner (node:test) (rejected)
  Rejected because: Limited feature set, less mature ecosystem, fewer assertion libraries, and lacks the developer experience features present in the detected pattern
  When valid: For minimal projects with simple testing needs and desire to avoid external dependencies
- Use AVA test runner (rejected)
  Rejected because: Isolated test execution model increases overhead, less widespread adoption, and doesn't match the pattern characteristics observed in the 57 test files
  When valid: For projects requiring strict test isolation or when concurrent test execution is a primary concern

## Risks

- Framework adoption risk if Vitest development slows or project is abandoned
  Mitigation: Monitor project health metrics, maintain abstraction layer for test utilities, and establish fallback migration plan to Jest if needed
  Owner: Engineering team lead
- Inconsistent test execution across different environments due to ESM/TypeScript configuration variations
  Mitigation: Standardize tsconfig.json and vitest.config.ts across packages, document configuration requirements, and validate in CI pipeline
  Owner: DevOps team
- Developer resistance due to unfamiliarity with Vitest API or tooling
  Mitigation: Provide training materials, create example test templates, leverage Jest API compatibility mode, and establish testing best practices documentation
  Owner: Engineering team lead

## Implementation Notes

- Create a shared vitest.config.ts at the workspace root that can be extended by individual packages, ensuring consistent configuration across the monorepo
- Establish test file templates for common scenarios (unit tests, async tests, error handling) to accelerate test creation and maintain consistency
- Configure package.json scripts with 'test', 'test:watch', and 'test:coverage' commands using Vitest CLI for consistent developer workflow
- Set up CI pipeline integration with Vitest's --reporter=json option for test result parsing and coverage reporting
- Document migration path for any existing Jest tests, including API differences and common gotchas

## Continuation Context


Verify commands:
- find . -name '*.test.ts' -type f | head -5
- grep -r "from 'vitest'" --include='*.test.ts' | head -3
- test -f vitest.config.ts && echo 'Vitest config found' || echo 'Vitest config missing'
- npm list vitest 2>/dev/null || pnpm list vitest 2>/dev/null || yarn list vitest 2>/dev/null

Accept when:
- Test files with .test.ts extension are found in tests/ directories within packages
- Vitest imports are present in test files (e.g., import { describe, it, expect } from 'vitest')
- vitest.config.ts configuration file exists at workspace or package level
- Vitest is listed as a dependency in package.json and can be executed via npm/pnpm/yarn scripts

## Enforcement

- Verified by: CI pipeline runs test suite on every pull request and verifies all tests pass
- Verified by: Code review checklist includes verification of test file naming conventions and organization
- Verified by: Automated linting rules check for .test.ts extension on test files
- Verified by: Package.json scripts are validated to use Vitest commands rather than other test runners
- Violation handling: Pull requests with incorrectly named test files (not using .test.ts) are blocked by CI checks
- Violation handling: Code review feedback is provided for tests not following the established directory structure
- Violation handling: Tests using non-standard frameworks trigger automated comments suggesting migration to Vitest
- Violation handling: Quarterly audits identify non-compliant test files and create migration tickets
- Exception process: Developer submits exception request via architecture review board with justification
- Exception process: Tech lead reviews request and assesses impact on testing consistency and maintenance
- Exception process: If approved, exception is documented in package README with expiration date or migration plan
- Exception process: Exceptions are reviewed quarterly to determine if they can be resolved or need renewal