# Customization Guide

This guide shows how to adapt the framework to a new repo without losing the structure that makes it effective.

## Recommended Path

1) Run the one-time customization prompt:
   - `Open agents/_customize.md and follow instructions.`
2) Fill project-specific placeholders in:
   - `AGENTS.md`
   - `agents/outline.md`
   - `agents/spec.md`

## Remove Project-Specific Skills

Many starter skills are intentionally generic, but some may not apply to your repo. Remove or replace any skill that does not match your stack or constraints.

Keep skills that reflect repeatable workflows (e.g., compose changes, audit passes, small-diff discipline).

## Add Project-Specific Roles

If your repo has unique concerns, create roles that match them (e.g., data engineer, ML infra, compliance reviewer).

Use:
- `agents/prompts/role_create.md`

## Add Project-Specific Skills

For recurring workflows that must be done safely, create a new skill and example:
- `agents/prompts/skill_create.md`

## Update the Skills Index

Every new skill should be registered in:
- `agents/skills/skills_index.md`

This keeps discovery consistent for future agents.

## Typical Customizations

- Update `agents/outline.md` with accurate service boundaries.
- Update `agents/expectations.md` with non-functional requirements.
- Add project-specific runbooks under `docs/`.
