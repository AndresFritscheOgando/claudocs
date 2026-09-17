# Java Conventions

Target Java 21 unless the repository explicitly requires another version.

## General

- Use clear domain-oriented names.
- Classes: `PascalCase`.
- Methods and variables: `camelCase`.
- Constants: `UPPER_SNAKE_CASE`.
- Packages: lowercase.
- Prefer immutability where practical.
- Keep methods focused on one clear responsibility.
- Avoid arbitrary line-count limits; optimize for clarity and cohesion.
- Prefer composition over inheritance.
- Use exceptions for exceptional conditions, not normal control flow.

## Package structure

Default layered structure for general services:

```text
com.company.project
├── controller
├── service
├── repository
├── domain
├── dto
├── mapper
├── exception
└── config
```

Use the repository's established structure when one already exists.

## DTOs

Use explicit boundary DTOs.

Naming:

```text
EntityRequestDTO
EntityResponseDTO
```

Examples:

```text
UserRequestDTO
UserResponseDTO
PaymentRequestDTO
PaymentResponseDTO
```

Do not expose JPA entities directly through external API contracts.

## Interfaces

Do not create `Service` + `ServiceImpl` automatically.
Create an interface when there is a meaningful abstraction boundary, multiple implementations, pluggable infrastructure, or another concrete architectural reason.

## Dependency injection

Use constructor injection.
Dependencies should normally be `final`.
Avoid field injection.

## Lombok

Allowed when it improves clarity:

- `@Getter`
- `@Builder`
- `@RequiredArgsConstructor`

Avoid blanket `@Data` on JPA entities and important domain models.

## Null and errors

Prefer validation and explicit exceptions for invalid application states.
Do not use `Optional` as a normal entity field or method parameter.
Use `Optional` primarily for return values where absence is expected and meaningful.

## JPA / persistence

- Prefer LAZY relationships unless eager loading is specifically justified.
- Avoid unnecessary bidirectional relationships.
- Be aware of N+1 queries.
- Keep transaction boundaries deliberate.
- Paginate large queries.
- Do not base entity equality on unstable mutable fields.
- Use database constraints for important invariants.
- UUID identifiers are acceptable when appropriate; follow the project's established identifier strategy.

# Spring Boot

## Controllers

- Keep controllers thin.
- Validate request DTOs.
- Delegate business work to services.
- Return explicit response models.

## Services

- Own application/business workflows.
- Do not mix transport concerns into services.
- Use `@Transactional` deliberately around appropriate consistency boundaries.

## Repositories

- Keep persistence logic in repositories.
- Prefer clear query methods.
- Avoid loading more data than required.

## Validation

Use Jakarta Bean Validation for boundary input validation where appropriate.
Do not rely only on validation annotations for business invariants.

## Exceptions

Use specific application/domain exceptions.
Use centralized HTTP exception mapping, typically `@RestControllerAdvice`.
Do not return stack traces to API clients.

## Configuration

Use typed configuration properties for related configuration when practical.
Keep secrets out of code and source control.

## Testing

Use JUnit 5.
Use Mockito for isolated collaborators.
Use Spring Boot integration tests only when framework integration is part of what needs verification.
Use Testcontainers for real infrastructure integration when practical.
