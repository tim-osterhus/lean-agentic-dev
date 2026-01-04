# Lean Agentic Dev

A lightweight, project-agnostic framework for running agentic development with clear roles, repeatable prompts, and consistent logging.

## What This Gives You

- A standard way to run multi-agent work without chaos.
- A stable structure for task prompts, QA, and history logging.
- A repeatable onboarding flow that makes a repo “agent-ready.”

## How It Works (High Level)

The framework defines a small set of agent entrypoints and artifacts:

- **Builder**: implements tasks and small fixes quickly and safely.
- **QA**: verifies changes and records evidence.
- **Advisor**: handles freeform tasks like scoping work, explaining code, or drafting backlog task cards.

Builder/QA runs create or consume prompt artifacts, and every outcome is recorded in `agents/historylog.md`.

## Why It’s Useful

- **Clarity**: every agent knows where to look and how to proceed.
- **Traceability**: work is logged with context and evidence.
- **Repeatability**: you can reuse the workflow across repos and teams.

## One-Time Setup (Recommended)

Use this once per repo to make the framework project-specific.

1) Start an agentic coding session at the root of your target repo.
2) Say: `Open agents/_customize.md and follow instructions.`
3) The agent generates `agents/spec.md` and fills out key project files.

After setup, the repo is ready for day-to-day agentic work.

## Detailed Features and Workflows (In Full-Cycle Order)

This section follows the sequence you would encounter in a real workflow cycle.

### 1) Scope the Work (Advisor Session)

The Advisor is a dedicated, freeform session used to make the rest of the cycle clean and scoped.

Typical Advisor outputs:
- A set of task cards that are small and executable.
- A short explanation of how a subsystem works.
- A recommendation memo with options and tradeoffs.

The Advisor should use `agents/_advisor.md`, rely on `agents/outline.md` as the primary repo overview, and place any task cards in `agents/tasksbacklog.md` (not `agents/prompts/tasks/`).
Advisor runs only log to `agents/historylog.md` when they perform concrete actions beyond writing task cards.
When needed, the Advisor can also generate new roles and skills using the dedicated creation prompts.

### 2) Author Task Prompts (Prompt Engineering Cycle)

Task prompts are the central artifacts of the framework. Each task becomes a prompt file that can be executed without re-planning.

Core flow:
1) Create a task prompt with `agents/prompts/create_prompt.md`.
2) Store it in `agents/prompts/tasks/`.
3) Execute it with `agents/prompts/run_prompt.md`.
4) Archive it to `agents/prompts/completed/` after execution.

This is what makes the workflow repeatable and reviewable.

### 3) Build and Quickfix (Builder Session)

The Builder runs the task prompt and makes the smallest viable change set.

Builder guidance:
- Use `agents/_start.md`.
- Keep changes minimal and scoped to the task.
- Prefer safe, reviewable diffs.

Quickfixes use the same session but follow `agents/prompts/quickfix.md` for narrow, urgent changes.

### 4) QA and Verification (QA Session)

QA is a first-class session with its own entrypoint and verification flow.

Key pieces:
- `agents/_check.md` defines the QA flow.
- `agents/expectations.md` is an explicit expectations list used to anchor QA. This is a deliberate feature: it produces measurably stronger QA output because the agent verifies against concrete, written expectations rather than generic “check for issues.”
- QA results should be logged with evidence (commands, outputs, or screenshots).

### 5) Roles and Specialization

Roles are defined in `agents/roles/` and used when a task benefits from a specific lens (security, infra, QA, etc.). Use one role at a time, and switch explicitly.

Roles make multi-agent collaboration more predictable and reduce churn.
If a new role is needed, use `agents/prompts/role_create.md` to generate a role file that matches the repo’s conventions.
Most roles are broadly reusable across projects.

### 6) Skills (Reusable Procedures)

Skills are reusable playbooks stored under `agents/skills/`.

How they work:
- Each skill defines a specific workflow, constraints, and outputs.
- If a task matches a skill, the agent should follow it rather than improvising.
- Skills are meant to reduce risk and improve consistency across repos.
If a new skill is needed, use `agents/prompts/skill_create.md` to generate the skill and example scaffold.
Note: several starter skills are often project-specific and can be removed during customization.

### 7) History Logging

Every session prepends to `agents/historylog.md` (newest first) with a short summary, files touched, decisions, and follow-ups. This makes agent work auditable and easy to resume.

## Files Worth Reading

- `quickstart.md` — step-by-step usage guide
- `AGENTS.md` — main agent entrypoint and guardrails
- `agents/_customize.md` — one-time onboarding prompt
