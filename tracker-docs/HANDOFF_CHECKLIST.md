# Handoff Checklist

Use this before ending a work session or switching tools.

## Before You Stop

1. Update `CURRENT_TASK.md` — what is the state now and what is next
2. Append a short entry to `SESSION_LOG.md`
3. Update `DECISIONS.md` if a durable choice was made
4. Update `TODO.md` if any item status changed
5. Note any files that changed

## If Switching Tools (Claude Code ↔ Codex)

1. Make sure both tools point at the same folder containing `tracker-docs/`
2. Tell the new tool to read:
   - `tracker-docs/README.md`
   - `tracker-docs/CURRENT_TASK.md`
   - `tracker-docs/DECISIONS.md`
   - `tracker-docs/TODO.md`
3. Continue from there — no manual file copying needed if both share the same workspace

## If Switching To A Browser Chat (No File Access)

Paste only:
1. `PROJECT_CONTEXT.md`
2. `CURRENT_TASK.md`
3. Relevant parts of `DECISIONS.md`
4. The specific section of `index.html` relevant to the question

## If The Session Dies Unexpectedly

Use `RECOVERY_PROMPT.md`.
