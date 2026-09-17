# Error Handling Conventions

- Handle errors at the layer capable of doing something meaningful about them.
- Never silently swallow exceptions or rejected promises.
- Do not use exceptions for normal control flow.
- Do not expose stack traces or internal implementation details to clients.
- Translate low-level infrastructure failures into meaningful application errors at appropriate boundaries.
- Prefer specific domain or application exceptions over generic runtime failures.
- Log an error once at the appropriate boundary instead of repeatedly at every layer.
- Preserve the original cause when wrapping exceptions.

For APIs, return stable error codes that clients can reason about.
