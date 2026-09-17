# Change Documentation Workflow

Every completed logical code task must have a Markdown change record.

## Before implementation

1. Read this workflow.
2. Read `README.md` in this directory.
3. Read historical change records relevant to the area being modified.
4. Inspect the actual implementation and repository state.

## After implementation

1. Inspect the actual diff using repository tools such as `git status`, `git diff`, and changed source files.
2. Run the relevant verification for the change.
3. Create one new record using `TEMPLATE.md`.
4. Add the record to `README.md`.
5. Do not consider the task complete until both the implementation and the record are finished.

## Naming

Use:

```text
YYYY-MM-DD-short-kebab-case-description.md
```

Example:

```text
2026-09-17-add-refresh-token-rotation.md
```

## Scope

Create one record per logical task, not one record per modified file.
Split unrelated work into separate records.

## Evidence

Document what actually changed. Use the diff, source files, tests, build output, or other repository evidence.
Do not rely only on conversational memory.

## Verification language

Be precise:

- `Passed: ./mvnw test`
- `Passed: npm run lint`
- `Manual verification: login succeeds with valid credentials`
- `Not run: integration tests require unavailable external service`

Never claim verification that did not happen.
