# Tutorial: Add API Key Auth to a Flask API

This walkthrough demonstrates a full cycle using a fictional Flask API project. It shows the Advisor → Builder → QA flow and the artifacts produced along the way.

## Scenario

You have a simple Flask API with `/status` and `/search`. You want to add API key authentication to `/search` without changing other endpoints.

## Step 1: Advisor Scopes the Work

**Prompt to Advisor:**
"Open agents/_advisor.md and follow instructions. I need API key auth on /search."

**Advisor Output (added to `agents/tasksbacklog.md`):**

```
## Add API key auth to /search

- Goal: Require an API key for /search without changing /status
- Scope: Add middleware or decorator for /search only
- Out of scope: user signup, key rotation UI, OAuth
- Verification: curl with missing/invalid key returns 401; valid key returns 200
```

## Step 2: Promote Task

Move the task card into `agents/tasks.md` as the single active task.

## Step 3: Create the Prompt Artifact

**Prompt to Prompt Engineer:**
"Open agents/prompts/create_prompt.md and follow instructions."

**Result:** `agents/prompts/tasks/001-api-key-auth.md`

Key sections in the prompt:
- Objective: Require API key for `/search` only
- Files: `api/app.py`, `api/auth.py`, `tests/test_auth.py`
- Commands: `pytest tests/test_auth.py -v`

## Step 4: Builder Executes

**Prompt to Builder:**
"Open agents/_start.md and follow instructions."

Builder actions:
- Adds `api/auth.py` with `require_api_key` decorator
- Applies decorator to `/search` route
- Adds test cases for missing/invalid/valid keys

Builder logs to `agents/historylog.md` with files and verification commands.

## Step 5: QA Writes Expectations

**Prompt to QA:**
"Open agents/_check.md and follow instructions."

QA writes `agents/expectations.md` **before** inspecting code:

```
## Goal
Require API key for /search only.

## Expected Behavior
- /search returns 401 if API key missing or invalid
- /status remains public
- Valid API key returns 200 for /search

## Tests / Verification Commands
- curl -H "Authorization: Bearer bad" http://localhost:5000/search -> 401
- curl http://localhost:5000/status -> 200
- pytest tests/test_auth.py -v
```

## Step 6: QA Validates

QA inspects changes, runs tests, and logs pass/fail in `agents/historylog.md`.
If gaps exist, QA creates `agents/quickfix.md` and stops.

## Step 7: Archive Prompt

Move the executed prompt to `agents/prompts/completed/` and record completion in the history log.

## Result

You now have a complete, auditable workflow:
- Task scoped in backlog
- Prompt artifact created
- Changes implemented
- Expectations written first
- Verification logged with evidence
