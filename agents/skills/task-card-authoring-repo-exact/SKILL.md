---
name: task-card-authoring-repo-exact
description: >
  Writes a single, repo-accurate task card in `agents/tasks.md` (and optionally promotes from `agents/tasksbacklog.md`) that is executable by the Builder/QA cycles without interpretation.
---

# Task Card Authoring (Repo-Exact)

## Quick start
Goal:
- Produce one unambiguous task card that a Builder agent can execute end-to-end in a single cycle.

Use when (triggers):
- Creating or promoting a task in `agents/tasks.md`
- Turning vague user requests into repo-scoped work items
- Splitting a big initiative into 1-cycle deliverable slices
- The QA cycle produced gaps that need a new, tighter task card

Do NOT use when (non-goals):
- Multi-week roadmaps or broad brainstorming (use `agents/tasksbacklog.md` instead)
- Refactoring the agent framework itself

## Operating constraints
- No secrets: never embed API keys, tokens, passwords, private URLs.
- Be minimal: smallest diffs; no drive-by refactors unless required.
- Be explicit: state assumptions and verify them where possible.
- Be deterministic: prefer exact commands/checklists over vague guidance.
- Keep SKILL.md short: if you exceed ~500 lines, split details into linked files.

## Inputs this Skill expects
Required:
- `outline.md` (repo map) and at least one relevant file path to change
- Current `agents/tasks.md` (to avoid conflicting/duplicate tasks)

Optional:
- `agents/tasksbacklog.md` candidate task to promote
- `agents/expectations.md` and `agents/quickfix.md` if this is a QA-follow-up task
- Relevant logs or failing test output

If required inputs are missing:
- Ask for the MINIMUM missing info OR proceed with safest defaults and list assumptions.

## Output contract
Primary deliverable:
- Edits to `agents/tasks.md` that define ONE active task with clear DONE checks and file targets.

Secondary deliverables (only if needed):
- Optional: move the chosen backlog item from `agents/tasksbacklog.md` into `agents/tasks.md` (do not duplicate)
- Optional: add a 1–3 line note in `agents/historylog.md` explaining why the task exists

Definition of DONE (objective checks):
- [ ] `agents/tasks.md` contains exactly one active task card with file paths + commands
- [ ] DONE checks are objective and runnable (commands included)
- [ ] Task scope fits one Builder cycle (or explicitly calls out a safe cutoff)

## Procedure (copy into working response and tick off)
Progress:
- [ ] 1) Confirm scope + constraints
- [ ] 2) Locate entrypoints + relevant files
- [ ] 3) Plan smallest safe change set
- [ ] 4) Implement changes
- [ ] 5) Validate locally
- [ ] 6) Summarize changes + next steps

### 1) Confirm scope + constraints
- Restate objective in ONE sentence.
- List constraints (security, production offline/LAN-only, no new deps, etc.).
- List assumptions explicitly.

### 2) Locate entrypoints + relevant files
Run targeted searches:
- Search terms:
  - agents/tasks.md
  - tasksbacklog.md
  - expectations.md
  - quickfix.md
  - historylog.md
- Files to inspect first (prioritized):
   1) agents/tasks.md
   2) agents/tasksbacklog.md
   3) agents/_start.md or agents/_advisor.md (depending on task)
   4) agents/prompts/builder_cycle.md

### 3) Plan smallest safe change set
Rules:
- Touch the minimum number of files.
- Prefer additive changes over rewrites.
- If multiple approaches exist, choose the simplest that satisfies DONE checks.
- If risk is medium/high, write a micro-plan artifact before coding (see “Verification pattern”).
- If the task touches retrieval/infra/security, add a “Verification pattern” subsection in the task card.
- Reference concrete paths under `rag_api/`, `infra/`, or `librechat/` (no “update the backend” phrasing).

### 4) Implement changes
Implementation checklist:
- [ ] Follow repo conventions (naming, formatting, module boundaries).
- [ ] Add or adjust any needed configuration.
- [ ] Update tests where applicable.
- [ ] Update docs where user-facing behavior changes.
- [ ] Task card includes the exact validation commands the Builder must run.

### 5) Validate locally (choose what exists in the repo)
Run validations in this order:
1) Fast static checks:
   - markdown lint (if configured) OR manual scan for broken headings/checkboxes
2) Unit/targeted tests:

3) Integration smoke test:


If validation fails:
- Do not guess. Inspect error output, fix, re-run until green.
- If blocked by missing deps or environment, document the exact missing item and minimal install/run step.

### 6) Summarize changes + next steps
Include:
- What changed (bullets)
- Why (bullets)
- How to verify (exact commands)
- Next steps (1–3 max)

## Pitfalls / gotchas (keep this brutally honest)
- Writing tasks as narratives instead of checklists → enforce explicit file targets + numbered steps.
- DONE checks that are subjective (“looks good”) → require commands + expected outputs.
- Packing multiple unrelated changes into one card → split by subsystem (RAG API vs LibreChat vs infra).

## Progressive disclosure (one level deep)
If this Skill needs detail, link it directly from HERE (avoid chains of references):
- Advanced workflow: ./advanced.md

## Verification pattern (recommended for medium/high risk)
Use this when changes touch infra, retrieval logic, licensing, or security:
1) Analyze
2) Write a machine-checkable plan artifact (e.g. report.md / changes.json)
3) Validate assumptions (paths, versions, config)
4) Execute changes
5) Verify DONE checks

## Optional: scripts section (ONLY if repo already uses scripts)
Run:
- bash scripts/run_cycle.sh builder

Expected output:
- Builder produces code + verification commands

Common failures:
- Script missing/permissions → `chmod +x scripts/run_cycle.sh`

## Example References (concise summaries only)

**How to reference examples:**
- Keep summaries SHORT (1-2 sentences max)
- Include line number reference to EXAMPLES.md
- Agents will load full examples only when symptoms match

**Example summaries:**

1. **Promote backlog item into active task** - Move ONE item from backlog, rewrite with explicit paths and commands. See EXAMPLES.md:7-68
2. **Split vague multi-feature request** - Split "hybrid retrieval and reranking" into separate cards with precision@k reports. See EXAMPLES.md:71-164

**Note:** Full examples with tags and trigger phrases are in `./EXAMPLES.md`.
Agents search that file only when they encounter matching symptoms (context-efficient).
