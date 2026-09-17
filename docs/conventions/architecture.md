# Architecture Conventions

Scope: backend/service architecture. Frontend structure (component organization,
state management, etc.) is documented separately.

- Prefer simple solutions over premature abstractions.
- Do not introduce a new architectural pattern when an established equivalent already exists.
- Keep business logic separate from transport, persistence, and framework concerns where practical.
- Avoid circular dependencies.
- Prefer composition over inheritance.
- Do not create abstractions for hypothetical future requirements.
- Keep module boundaries explicit.

## Default topology

- Default to a modular monolith: one deployable, internally split into clear modules
  (bounded contexts) with explicit boundaries between them.
- Split a module out into its own service only when there's a concrete reason to
  (independent scaling, independent deployment cadence, separate team ownership,
  a genuinely different runtime need). Don't default to microservices.

## Layering (Clean Architecture)

- Controllers: coordinate requests (parse input, call a use case, shape the response).
  No business logic here.
- Use cases: one per business workflow/operation. Orchestrate domain logic and
  call out to ports (interfaces) for anything external.
- Domain: entities and business rules. Must not depend on frameworks, transport,
  or persistence details.
- Repositories: implement the persistence ports the domain/use-case layer defines.
  They own persistence access; nothing above them talks to the database directly.
- Dependency direction always points inward: infra/transport depend on the domain,
  never the reverse.

## Module boundaries and data ownership

- Each module owns its own schema/tables within the monolith's database.
- Cross-module access goes through the owning module's use-case/service API —
  never by querying another module's tables directly.
- If a module is later split into its own service, this boundary already holds:
  a service owns its own data, and other services reach it through its API, not
  its database.

## Communication defaults

- REST: external/client-facing synchronous APIs.
- gRPC: internal synchronous service-to-service communication when justified
  (once you've actually split services out of the monolith).
- Kafka/event messaging: asynchronous domain events and decoupled workflows.

Use the mechanism that best matches the interaction instead of forcing one technology everywhere.

## Async/event workflows

- Default to simple pub/sub: a module/service publishes a domain event, others
  consume it independently. No central orchestrator by default.
- Reach for orchestration/sagas only when a multi-step workflow genuinely needs
  coordinated compensation logic across steps — don't introduce a workflow engine
  preemptively.

## Stack notes

- Primary backend stacks: Node.js/TypeScript and Java (Spring Boot). Frontend
  (React/Next.js) architecture is out of scope for this document.
- These conventions are written to be stack-agnostic where possible; apply the
  same layering and boundary rules regardless of which of the two stacks a
  given service uses.
