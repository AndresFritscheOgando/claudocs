# Project Workflow Starter

Reusable engineering workflow for every new project.

## Install

Copy the contents of this folder into the root of a repository.

```text
project/
├── AGENTS.md
├── CLAUDE.md
└── docs/
    ├── changes/
    └── conventions/
```

If the repository already contains `AGENTS.md` or `CLAUDE.md`, merge these rules instead of overwriting existing project-specific instructions.

## Operating model

Before coding, agents must:

1. Read `AGENTS.md`.
2. Read only the convention files relevant to the task.
3. Inspect existing code and preserve established local patterns unless the task requires otherwise.
4. Read relevant entries from `docs/changes/README.md` and any linked change records that affect the area being modified.

After coding, agents must:

1. Review the actual diff.
2. Run relevant verification.
3. Create one change record per logical task in `docs/changes/`.
4. Update `docs/changes/README.md`.
5. Treat the task as incomplete until the change record exists.

## Precedence

When rules conflict, use this order:

1. Explicit task instructions.
2. Project-specific repository rules.
3. Existing local code patterns for existing code.
4. These generic conventions for new code.

Do not refactor unrelated code merely to make it match these conventions.
