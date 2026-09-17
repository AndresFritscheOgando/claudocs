# Engineering Agent Instructions

These rules apply to AI coding agents working in this repository.

## Mandatory workflow

Before modifying code:

1. Understand the task and expected outcome.
2. Inspect the existing implementation before proposing a new pattern.
3. Read only the relevant convention files under `docs/conventions/`.
4. Read `docs/changes/README.md` and any relevant historical records when the task touches an area with prior documented decisions.
5. Prefer the smallest change that fully solves the task.

While modifying code:

- New code must follow the conventions in this repository.
- Existing code keeps its current style unless the task requires changing it.
- Do not refactor unrelated code.
- Do not introduce a new architectural pattern, dependency, abstraction, or naming convention when an established equivalent already exists.
- Do not silently change public contracts.
- Do not add dependencies without checking whether the existing stack already solves the problem.
- Do not invent requirements.

After modifying code:

1. Inspect the actual diff.
2. Run relevant tests, static analysis, formatting, or build checks.
3. Report verification truthfully. Never claim a check passed unless it ran successfully.
4. Create or update exactly one logical change record in `docs/changes/` for the completed task.
5. Update `docs/changes/README.md`.
6. Treat the implementation as incomplete until the documentation step is finished.
7. After every output, you should explain briefly the user what was done and why.
## Convention routing

Read only what applies:

- Java / Spring Boot: `docs/conventions/java.md`
- TypeScript / React / Next.js: `docs/conventions/typescript.md`
- Tailwind CSS / UI styling: `docs/conventions/tailwind-css.md`
- Architecture: `docs/conventions/architecture.md`
- API design: `docs/conventions/api.md`
- Database / persistence: `docs/conventions/database.md`
- Error handling: `docs/conventions/error-handling.md`
- Security: `docs/conventions/security.md`
- Testing: `docs/conventions/testing.md`
- Logging: `docs/conventions/logging.md`
- Observability: `docs/conventions/observability.md`
- Configuration: `docs/conventions/configuration.md`
- Docker: `docs/conventions/docker.md`
- Dependencies: `docs/conventions/dependencies.md`
- Documentation: `docs/conventions/documentation.md`
- Git workflow: `docs/conventions/git-workflow.md`
- Commit messages: `docs/conventions/commits.md`
- Agent behavior: `docs/conventions/agent-development.md`

## Precedence

1. Explicit task instructions.
2. Repository-specific rules.
3. Existing local patterns for existing code.
4. Generic conventions for new code.

Do not use these conventions as justification for unrelated cleanup.
