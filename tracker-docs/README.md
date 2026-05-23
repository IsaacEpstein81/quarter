# Tracker Docs

This folder is the shared project memory for the 15-Min Tracker app.

Point Claude Code or any AI tool at the parent folder and it can read all of these files without you needing to paste context manually.

## Where The Code Lives

The app files live wherever you put them after copying from the worktree. Recommended:

```text
~/projects/15min-tracker/
  index.html
  manifest.json
  sw.js
  tracker-docs/   ← this folder, or keep it here and reference it
```

Or keep `tracker-docs` here in `/Users/macbookair13/Documents/Business/quarter/quarter/tracker-docs` and just tell the AI to read it at session start.

## Read Order For Any New Session

1. `PROJECT_CONTEXT.md`
2. `CURRENT_TASK.md`
3. `DECISIONS.md`
4. `TODO.md`
5. `SESSION_LOG.md`

## Files In This Folder

- `README.md` — this file; docs index and orientation
- `PROJECT_CONTEXT.md` — what the app is, stack, what is built
- `ARCHITECTURE.md` — file structure and how the code is organized
- `DECISIONS.md` — durable decisions and the reasons behind them
- `MVP_EXECUTION_PLAN.md` — recommended build order for future features
- `CURRENT_TASK.md` — what is actively being worked on right now
- `SESSION_LOG.md` — short chronological handoff notes
- `TODO.md` — master feature backlog and checklist
- `DAILY_STARTUP_PROMPT.md` — copy-paste prompt for a fresh coding session
- `END_OF_SESSION_PROMPT.md` — copy-paste prompt for wrapping up a session
- `RECOVERY_PROMPT.md` — copy-paste prompt after an interrupted session
- `HANDOFF_CHECKLIST.md` — checklist before ending or switching tools
- `AI_WORKFLOW.md` — how to work efficiently across sessions without burning context

## Minimum Update Rules

- Update `CURRENT_TASK.md` whenever the active focus changes.
- Update `SESSION_LOG.md` after each meaningful work block or before stopping.
- Update `DECISIONS.md` when a choice has lasting consequences.
- Update `TODO.md` when feature status actually changes.
