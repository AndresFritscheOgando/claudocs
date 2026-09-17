# Log Change Specification

## Intent

Produce the change-history record this repo's `AGENTS.md`/`docs/changes/WORKFLOW.md` workflow already requires after a logical task finishes, so no completed task goes undocumented in `docs/changes/`.

## Scope

In scope:
- Reading the current working-tree diff as evidence.
- Drafting one `docs/changes/<date>-<slug>.md` record per logical task, using the live `TEMPLATE.md` structure.
- Adding one row to `docs/changes/README.md`.

Out of scope:
- Implementing the change itself, reading convention docs, or any other step of the AGENTS.md workflow prior to documentation.
- Committing or pushing the resulting files.
- Deciding whether a task is "done" — the user invokes this skill only after that.

## Users And Trigger Context

- Primary users: contributors to this repo finishing a task under the AGENTS.md workflow.
- Common user requests: "log this change", "write the change record", "update the change history", "/log-change".
- Should not trigger for: mid-task requests, or any request where no code/doc change has actually been made yet. `disable-model-invocation: true` keeps this manual-only.

## Runtime Contract

- Required first actions: `git status` / `git diff` / `git diff --staged`; read `docs/changes/WORKFLOW.md`, `README.md`, `TEMPLATE.md`.
- Required outputs: one new `docs/changes/*.md` file plus an updated `README.md` row, shown to the user before writing.
- Non-negotiable constraints: verification claims must be backed by checks actually run in-session; one record per logical task.
- Expected bundled files loaded at runtime: none — the skill intentionally reads the repo's own `docs/changes/` files live instead of duplicating their structure.

## Source And Evidence Model

Authoritative sources:
- `docs/changes/WORKFLOW.md`, `docs/changes/README.md`, `docs/changes/TEMPLATE.md` (read fresh each run).
- `git status` / `git diff` output for the current working tree.

Data that must not be stored: none collected beyond the repo's own tracked files.

## Reference Architecture

- `SKILL.md` contains: the full runtime procedure (single coherent flow, no branching depth needed).
- No `references/`, `scripts/`, or `assets/` — the skill has one dominant path and no optional deep knowledge.

## Validation

- Lightweight validation: `scripts/quick_validate.py` from the `skill-writer` skill (structural check on frontmatter/paths).
- Acceptance gate: the drafted record matches the live `TEMPLATE.md` sections and the README table stays in reverse chronological order.

## Known Limitations

- Relies on the user's conversation history to know which verification commands actually ran; cannot independently confirm that.
- Does not detect when a diff spans multiple unrelated logical tasks beyond flagging it for the user to decide.

## Maintenance Notes

- Update `SKILL.md` if `docs/changes/WORKFLOW.md` or `TEMPLATE.md`'s structure changes in a way that requires new runtime steps (not just content, since those are read live).
- Update this `SPEC.md` if the skill's scope changes (e.g., it starts also committing files, or supporting multiple records per invocation).
