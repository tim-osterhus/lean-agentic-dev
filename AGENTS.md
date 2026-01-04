# Project — Agents Hub

**Purpose.** Single, stable entry point for any coding agent. This is the repo-specific context you want an `/init` to load: what the stack is, how the agent workflow runs, and where to write outcomes.

---

## 1) Core context (project-specific)

- **What this repo is:** <one sentence describing the product/system and its purpose>.
- **Production target:** <deployment constraints, e.g., offline-only, regulated, latency goals>.
- **Guardrails:** <data handling, safety/compliance, or review requirements>.
- **Review gates:** <human review or QA gates required before shipping>.

---

## 2) How work enters the system

1) **Read the active task:** `agents/tasks.md` (single source of truth).
2) **Use the entrypoints:** `agents/_start.md` for Builder, `agents/_check.md` for QA, `agents/_advisor.md` for freeform advisory work.
3) **Use prompt artifacts:** create via `agents/prompts/create_prompt.md`, run via `agents/prompts/run_prompt.md`.

If there is no active task, stop and ask for one.

---

## 3) Standard workflow (advisor → builder → QA → log)

1) **Scope:** use Advisor to draft backlog task cards in `agents/tasksbacklog.md` when the request is unclear or large.
2) **Plan:** derive a task prompt artifact (under `agents/prompts/tasks/`) when ready to execute.
3) **Build:** execute the prompt; make the smallest viable changes.
4) **QA:** run `agents/prompts/qa_cycle.md` when applicable.
5) **Document:** Builder/QA runs prepend a concise summary to `agents/historylog.md` (newest first). Advisor runs only log when performing concrete actions beyond writing task cards.
6) **Archive:** move executed prompts to `agents/prompts/completed/`.

---

## 4) Roles and specialization

Roles are defined in `agents/roles/` (one file per role). Use one role at a time and switch explicitly between roles if needed.

---

## 5) Non-negotiables (safety + quality)

- **Environment constraints:** respect deployment limits (offline, air-gap, latency, cost).
- **Data handling:** follow privacy, security, and compliance requirements.
- **Quality gates:** do not ship without required verification and review.
- **No secrets** in repo or logs.

---

## 6) Output + logging requirements

Every Builder/QA run **must** prepend to `agents/historylog.md` (newest first). Advisor runs only log when performing concrete actions beyond writing task cards:

`[YYYY-MM-DD] AgentName • Task Title`

- Summary (1–3 sentences)
- Files touched
- Decisions/tradeoffs
- Follow-ups
- Prompt reference (if applicable)

---

## 7) Where to look for details

- **Architecture map:** `agents/outline.md`
- **Quickstart:** `quickstart.md`
- **Backlog:** `agents/tasksbacklog.md`
- **QA artifacts:** `agents/expectations.md`, `agents/quickfix.md`
- **Skills library:** `agents/skills/` and `agents/skills/skills_index.md`
- **Role/skill creation:** `agents/prompts/role_create.md`, `agents/prompts/skill_create.md`

---

## 8) Model-specific wrappers

- **Claude agents →** see `CLAUDE.md`
- **Gemini agents →** see `GEMINI.md`

---

## 9) Why these constraints exist

- Production constraints protect customers and operations.
- Explicit guardrails prevent accidental regressions.
- The history log is the continuity layer between agents and sessions.
