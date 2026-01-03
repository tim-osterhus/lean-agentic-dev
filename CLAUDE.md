# Claude Agent Guide (Wrapper)

Read `agents/agents.md` first. It is the single source of truth.

Claude-specific notes:
- Prefer concise reasoning in outputs; include only decisions, diffs, and commands.
- Keep edits minimal and scoped; avoid refactors unless asked.
- If sources are insufficient, return “insufficient evidence” with next steps.
