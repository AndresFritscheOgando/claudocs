# AI Development Conventions

## Before coding

- Read repository instructions.
- Inspect existing implementations before creating new patterns.
- Read only the conventions relevant to the task.
- Read relevant change history when prior decisions may matter.
- Identify the smallest change that satisfies the requirement.

## During coding

- Do not refactor unrelated code.
- Do not introduce duplicate abstractions.
- Do not add dependencies without justification.
- Do not change public contracts silently.
- Do not invent new requirements.
- Prefer existing project patterns when they do not conflict with mandatory rules.
- Keep edits scoped to the task.

## After coding

- Review the diff.
- Run relevant verification.
- Check for accidental unrelated changes.
- Update the change journal.
- State limitations or unrun checks explicitly.
