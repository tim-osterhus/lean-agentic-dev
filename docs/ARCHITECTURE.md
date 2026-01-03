# Architecture

This framework provides a stable structure for running agentic development in a repo. It focuses on clear entrypoints, repeatable artifacts, and auditable outcomes.

## Core Components

### 1) Entry Points (Agent Roles)

- `agents/_start.md` — Builder entrypoint. Implements scoped changes and runs minimal verification.
- `agents/_check.md` — QA entrypoint. Writes expectations first, then validates against reality.
- `agents/_advisor.md` — Advisor entrypoint. Scopes work, explains systems, and drafts backlog tasks.

### 2) Task Artifacts

- `agents/tasks.md` — single active task card for the current cycle.
- `agents/tasksbacklog.md` — backlog of future tasks or larger items.
- `agents/prompts/tasks/` — prompt artifacts that the Builder executes.
- `agents/prompts/completed/` — executed prompt artifacts, archived for traceability.

### 3) QA Artifacts

- `agents/expectations.md` — the QA contract written before inspection.
- `agents/quickfix.md` — gaps or defects discovered by QA.

### 4) History and Continuity

- `agents/historylog.md` — an append-only log of Builder/QA outcomes.
- `agents/outline.md` — repo map and system overview used as primary context.

## Workflow Overview

1) Advisor scopes work and drafts backlog items in `agents/tasksbacklog.md`.
2) A task card is promoted into `agents/tasks.md`.
3) A prompt artifact is authored in `agents/prompts/tasks/`.
4) Builder executes the prompt and logs outcomes.
5) QA writes expectations, validates work, and logs evidence.
6) Prompt artifacts are archived to `agents/prompts/completed/`.

## Design Contracts

- The Builder must keep diffs small and scoped to the task card.
- QA must define success criteria before inspecting implementation.
- History logs must capture what changed, why, and how it was verified.

## Folder Layout

```
repo-root/
├── AGENTS.md
├── quickstart.md
├── agents/
│   ├── _start.md
│   ├── _check.md
│   ├── _advisor.md
│   ├── _customize.md
│   ├── expectations.md
│   ├── historylog.md
│   ├── outline.md
│   ├── tasks.md
│   ├── tasksbacklog.md
│   ├── prompts/
│   │   ├── create_prompt.md
│   │   ├── run_prompt.md
│   │   ├── qa_cycle.md
│   │   ├── quickfix.md
│   │   ├── tasks/
│   │   └── completed/
│   ├── roles/
│   └── skills/
└── docs/
```

## Why This Works

The structure enforces separation of concerns:
- Advisor defines scope.
- Builder implements.
- QA verifies with expectations written before inspection.

This minimizes bias, reduces scope creep, and makes agent output auditable.
