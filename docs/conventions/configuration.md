# Configuration Conventions

- Externalize environment-specific configuration.
- Never hardcode production credentials or environment-specific secrets.
- Keep secrets out of source control.
- Environment-specific configuration should not change core application logic.
- Provide safe local development defaults where practical.
- Fail clearly when required production configuration is missing.
- Configuration is fixed at startup/deploy time. Changing it means redeploying —
  don't build runtime hot-reload for config unless a specific value has a proven
  need for it.
- Configuration varies by environment only. There is no per-tenant/per-client
  configuration layer; tenant-specific behavior belongs in application data, not
  environment config.

## Secrets

- Secrets are injected as environment variables by the deploy platform (container
  orchestrator, PaaS, CI/CD pipeline) — no separate secret manager service by default.
- For local development, use a `.env` file that is gitignored; never commit it.
- Rotate and manage secrets at the platform level; application code only ever
  reads them as environment variables.

## Validation

- Validate configuration against a schema at startup and fail fast with a clear,
  specific error when a required value is missing or invalid.
  - Node.js/TypeScript: parse `process.env` into a typed config object with a
    schema validator (e.g. zod, Joi) once at startup.
  - Java/Spring Boot: bind configuration with `@ConfigurationProperties` and
    apply Bean Validation annotations so the context fails to start on invalid config.
- Read configuration through the validated config object; don't scatter raw
  `process.env` / `System.getenv()` access through business logic.

## Naming

- Prefix environment variables with the owning module/service name, e.g.
  `AUTH_DB_URL`, `BILLING_KAFKA_BROKER`. This mirrors module data ownership
  (see architecture conventions) and keeps ownership obvious as the app grows.
- Use `SCREAMING_SNAKE_CASE` for all environment variable names.

## Feature flags

- Out of scope for this document. If/when feature flags are introduced, they
  are documented separately rather than folded into environment configuration.

Typical environments may include:

```text
local
development
test
staging
production
```
