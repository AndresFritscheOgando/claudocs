# Commit Conventions

Use Conventional Commits with a mandatory scope:

```text
<type>(<scope>): <description>
```

Examples:

```text
feat(auth): add refresh token rotation
fix(payment): prevent duplicate capture
refactor(order): extract pricing policy
```

## Allowed common types

- feat
- fix
- refactor
- perf
- docs
- test
- chore
- ci
- build
- style

## Rules

- Scope is mandatory.
- Use imperative mood.
- Keep the subject concise; approximately 72 characters is a guideline, not a hard validator.
- One logical change should map to one commit when practical.
- Do not use vague messages such as `fix stuff`, `changes`, `updates`, or `final fix`.
- Add a body when context, migration steps, or rationale are useful.

## Breaking changes

Use `!` and explain the breaking change in the body:

```text
feat(api)!: change payment response schema

BREAKING CHANGE: `status` is now returned as a structured object.
```

AI agents must not create commits or push them unless explicitly instructed.
