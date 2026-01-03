# One-Time Customization Prompt

You are onboarding this agentic framework to a new project repo. Your job is to generate a project spec sheet and fill in the project-specific files so the system becomes immediately usable.

## Output Targets

Create or update these files:
- `agents/spec.md` (new) — context-heavy spec sheet
- `AGENTS.md` — project overview, guardrails, workflow
- `agents/outline.md` — repo outline and stack
- `agents/tasks.md` — initial task entry or placeholder
- `agents/roadmap.md` — high-level roadmap template filled for this repo
- `agents/expectations.md` — success criteria and verification notes

Keep all edits ASCII-only and minimal.

## Step 1: Repo Scan (fast)

Inspect the project repo to extract basics:
- Top-level folders and key entrypoints
- Primary languages/frameworks
- Build/test/lint commands (if present)
- Deployment or runtime constraints (from docs/configs)

If a README exists, skim it for setup and constraints.

If an `agents/outline.md` already exists, use it as the primary repo overview and only scan the repo directly if the outline is missing or outdated.

## Step 2: Ask for Missing Context

If any of the below are unknown, ask the user directly:
- One-sentence product description
- Deployment target (offline/online, regulated, SLAs)
- Data sensitivity and compliance constraints
- Review/approval gates (human review, QA, release)
- Critical non-negotiables (security, latency, cost)

Keep questions concise and in a single message.

## Step 3: Write the Spec Sheet

Create `agents/spec.md` with this structure:

1) Project Summary (3-7 bullets)
2) Users and Use Cases
3) Runtime Constraints (offline/online, latency, cost)
4) Data and Compliance Requirements
5) Architecture Overview (services, databases, APIs)
6) Verification Commands (build/test/lint)
7) Operational Risks and Guardrails

Use concrete details from the repo or user answers. Mark unknowns explicitly as TODO.

## Step 4: Fill Project-Specific Files

Update the following using the spec sheet:
- `AGENTS.md`: replace placeholders with the project summary, constraints, and guardrails.
- `agents/outline.md`: include repo structure, stack, and verification commands.
- `agents/tasks.md`: add a single starter task or placeholder that reflects current priorities.
- `agents/roadmap.md`: add 2-4 realistic themes and near-term goals.
- `agents/expectations.md`: list verification expectations, evidence types, and quality gates.

Avoid changing files not listed above.

## Step 5: Create Project-Specific Roles and Skills (Required)

1) If the repo needs new roles, use `agents/prompts/role_create.md` to generate them.
2) If the repo needs new skills, use `agents/prompts/skill_create.md` to generate them.
3) Update `agents/roles/` and `agents/skills/skills_index.md` accordingly.
4) If no new roles/skills are needed, write a short note in `agents/spec.md` explaining why.

## Step 6: Confirm Completion

Summarize what you updated and list the files touched. Ask if the user wants to revise any sections.
