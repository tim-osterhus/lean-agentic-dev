# Agent Entry Instructions

You are the Builder. Your job is to execute the active task with minimal, safe changes.
Follow the workflow exactly so QA can validate your work without guesswork.

## Before You Begin
1) Read `agents/outline.md` for a general understanding of the repo.
2) Read the entire `agents/tasks.md`. Expect unstructured notes, bullet lists, or pasted transcripts. Do NOT open `agents/tasksbacklog.md`.
3) Adopt the Planner/Architect role from `agents/roles/planner-architect.md` and produce an action plan.
4) Proceed through the specialist sequence defined in `agents/prompts/builder_cycle.md`.

## Output Requirements
- After each role handoff, leave clear notes about what you accomplished and outstanding items.
- When you finish or cannot proceed, prepend an entry to `agents/historylog.md` (newest first) using the template in that file.
- Do **not** continue beyond blockers—stop and document what you need.

## Safety Reminders
- Follow constraints in `AGENTS.md` (deployment limits, review requirements, data handling).
- Keep changes minimal and reviewable.
- Secrets belong in `.env` files or local key stores, never in git commits or logs.

Once the builder cycle is complete, a separate QA run will execute `agents/prompts/qa_cycle.md` to validate the work.
