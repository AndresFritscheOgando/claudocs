---
name: log-change
description: Writes the dated change-history record in docs/changes/ for a just-completed engineering task, following this repo's existing docs/changes/WORKFLOW.md and TEMPLATE.md, and adds a row to docs/changes/README.md. Use when the user says a change/task is done and asks to log it, record it, document it, write a changelog entry, or update the change history. Manual, user-invoked only — never fires on its own.
disable-model-invocation: true
---

# Log Change

Produce the change-history record required by this repo's own workflow after a task is already implemented. Do not re-run the implementation workflow (convention reading, coding) — that happened before this skill runs.

## Steps

1. **Gather evidence.** Run `git status`, `git diff`, and `git diff --staged`. This diff is the source of truth — never invent content from conversational memory alone. If the working tree is clean and nothing is staged, tell the user there is nothing to log and stop.
2. **Read the current rules.** Read `docs/changes/WORKFLOW.md`, `docs/changes/README.md`, and `docs/changes/TEMPLATE.md` now, in this invocation — do not rely on remembered structure, since these files can change independently of this skill.
3. **Check logical scope.** Per WORKFLOW.md's Scope rule: one record per logical task, not one per file, and not one record bundling unrelated work. If the diff clearly mixes unrelated concerns, ask the user whether to split it into multiple records before writing anything.
4. **Draft the record** using the exact section structure read from `TEMPLATE.md` in step 2 (do not assume its sections — they may have been edited).
5. **Name the file** `YYYY-MM-DD-short-kebab-case-description.md` per WORKFLOW.md's Naming section, using today's actual date.
6. **Write verification honestly.** Only list checks (tests, lint, build, manual verification) that were actually run earlier in this conversation. Use the exact phrasing style from WORKFLOW.md:
   - `Passed: <command>`
   - `Not run: <reason>`
   Never mark something as passed that did not run. If unsure what was run, ask the user rather than guessing.
7. **Pick a Type** from the list in `docs/changes/README.md` (Feature, Fix, Refactor, Performance, Security, Infrastructure, Documentation, Test, Maintenance) or a similarly simple descriptive type if none fit.
8. **Show a preview.** Present the drafted record and the new README row to the user before writing, since this creates a repo-visible documentation file.
9. **Write the files:**
   - Create the new file under `docs/changes/`.
   - Add one new row to the table in `docs/changes/README.md`, keeping reverse chronological order.

## Guardrails

- One record per logical task — never split a single task across multiple files, never merge unrelated tasks into one.
- Never fabricate a passing check, a file path, or a reason for a change that isn't backed by the diff or the conversation.
- If `docs/changes/WORKFLOW.md`, `README.md`, or `TEMPLATE.md` don't exist at their expected paths, stop and tell the user — do not invent a replacement format.
