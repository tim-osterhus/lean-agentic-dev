# Quickstart

This guide shows how to use the framework end-to-end, exactly as intended.

## 1) Install the Framework in a Repo

1) Copy the contents of `lean-agentic-dev/` into the root of your target repo.
2) Ensure the `agents/` folder exists at repo root.
   - Example: `<repo-root>/AGENTS.md` and `<repo-root>/agents/_start.md`

If you already have an `agents/` directory, merge carefully and keep one set of entrypoints.

## 2) One-Time Customization (Recommended)

1) Start an agentic coding session at the root of your target repo.
2) Say: `Open agents/_customize.md and follow instructions.`
3) The agent scans the repo, asks any missing questions, and writes/edits:
   - `agents/spec.md`
   - `AGENTS.md`
   - `agents/outline.md`
   - `agents/tasks.md`
   - `agents/roadmap.md`
   - `agents/expectations.md`

After this step, the framework is tailored to your project.

## 3) Create or Update a Task

1) Edit `agents/tasks.md` and describe the current task.
2) If the work is large, ask the Advisor to break it into backlog task cards in `agents/tasksbacklog.md`.

## 4) Run the Three-Agent Workflow

### A) Builder / Quickfix Agent

1) Start a dedicated agentic session at repo root.
2) Say: `Open agents/_start.md and follow instructions.`
3) The Builder creates a detailed prompt artifact under `agents/prompts/tasks/` and executes it.

### B) QA Agent

1) Start a second dedicated agentic session at repo root.
2) Say: `Open agents/_check.md and follow instructions.`
3) The QA agent verifies the work and logs evidence.

### C) Advisor Agent (Freeform)

1) Start a third session at repo root.
2) Say: `Open agents/_advisor.md and follow instructions.`
3) Use this agent for scoping, research, explanations, backlog task-card creation, and any other odd jobs.
4) The Advisor should rely on `agents/outline.md` for repo context and only log to `agents/historylog.md` when performing concrete actions beyond writing task cards.
5) If you need new roles or skills, ask the Advisor to run `agents/prompts/role_create.md` or `agents/prompts/skill_create.md`.
