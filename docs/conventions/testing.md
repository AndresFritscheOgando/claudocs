# Testing Conventions

- Test behavior, not implementation details.
- Every bug fix should include a regression test when practical.
- Keep tests deterministic and independent of execution order.
- Do not test private methods directly.
- Avoid excessive mocking when real collaborators are cheap and deterministic.
- Test names must describe expected behavior.

## Test levels

1. Unit tests for isolated business logic.
2. Integration tests for persistence, messaging, HTTP, framework, and infrastructure boundaries.
3. End-to-end tests only for important user or business flows.

## Java defaults

- JUnit 5
- Mockito
- Spring Boot Test when framework integration is required
- Testcontainers for real infrastructure dependencies when practical

## TypeScript defaults

- Vitest or Jest according to the project
- React Testing Library for component behavior
- Playwright for important end-to-end flows
