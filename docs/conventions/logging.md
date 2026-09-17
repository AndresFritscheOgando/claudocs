# Logging Conventions

- Use the project's structured logging framework.
- Do not use ad-hoc `System.out.println` or permanent debugging `console.log` statements in production code.
- Logs should describe meaningful events.
- Include useful correlation identifiers when available, such as `traceId`, `requestId`, `orderId`, or equivalent domain identifiers.
- Never log secrets or sensitive values.

## Levels

- ERROR: operation failed and requires attention.
- WARN: abnormal or degraded condition that is recoverable.
- INFO: meaningful business or system event.
- DEBUG: diagnostic information useful during troubleshooting.
- TRACE: extremely detailed diagnostics.

Do not use ERROR or WARN for normal expected behavior.
