# Troubleshooting

This page lists common setup and workflow issues and how to resolve them.

## 1) No Active Task

**Symptom:** Builder or QA says no active task.

**Fix:**
- Add a single task card to `agents/tasks.md`.
- If unsure, ask the Advisor to draft items in `agents/tasksbacklog.md` first.

## 2) Outline Is Missing or Stale

**Symptom:** Advisor or Builder is unsure of repo structure.

**Fix:**
- Update `agents/outline.md` with current services, entrypoints, and verification commands.
- Use `agents/_customize.md` to regenerate if needed.

## 3) QA Blocked by Missing Tests

**Symptom:** QA cannot run any tests or validate behavior.

**Fix:**
- Document the absence of tests in `agents/expectations.md`.
- Add a minimal verification command or smoke check if possible.

## 4) Prompt Artifact Missing

**Symptom:** Builder is asked to execute a task but no prompt exists.

**Fix:**
- Use `agents/prompts/create_prompt.md` to generate a prompt artifact.
- Store it under `agents/prompts/tasks/`.

## 5) Quickfix Loops

**Symptom:** QA repeatedly finds the same issues after Quickfix.

**Fix:**
- Stop and re-scope the task.
- Add explicit acceptance criteria to `agents/tasks.md`.
- Ensure the Builder addresses each item in `agents/quickfix.md` one by one.

## 6) Historylog Not Updated

**Symptom:** No trace of what was done in a cycle.

**Fix:**
- Append a concise entry to `agents/historylog.md` with files touched and verification commands.

## 7) Agent Overreach

**Symptom:** The agent changes files not listed in the task card.

**Fix:**
- Re-run with tighter task scope and explicit in/out boundaries.
- Use the small-diff discipline skill to enforce minimal changes.
