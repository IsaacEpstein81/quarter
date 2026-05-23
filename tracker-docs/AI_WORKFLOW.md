# AI Workflow

This workflow is designed for building the tracker across multiple sessions without burning context every time.

## Core Idea

Keep the real project files in one folder and keep the shared memory in `tracker-docs/`.

Point Claude Code (or any AI tool) at the parent folder. It can read both the code and the docs without you copying anything.

## Best Way To Avoid Wasting Context

Use AI for decisions and code — not for rebuilding context from scratch every session.

- Keep context on disk in markdown files, not only in chat
- Keep tasks small and scoped
- Keep `CURRENT_TASK.md` current
- Write a short session log entry before you stop
- Record decisions once in `DECISIONS.md` so you do not re-argue them

## What To Update And When

| File | When to update |
|------|---------------|
| `CURRENT_TASK.md` | When the task starts, when direction changes, before stopping |
| `SESSION_LOG.md` | After each meaningful work block, or before stopping |
| `DECISIONS.md` | When a choice has lasting consequences |
| `TODO.md` | When item status actually changes |

## Starting A Session

Use the prompt in `DAILY_STARTUP_PROMPT.md`.

Short version:
```text
Read tracker-docs/README.md, CURRENT_TASK.md, DECISIONS.md, TODO.md, SESSION_LOG.md. Then summarize where we are and continue.
```

## Ending A Session

Use the prompt in `END_OF_SESSION_PROMPT.md`.

Short version:
```text
Update CURRENT_TASK.md, SESSION_LOG.md, DECISIONS.md, and TODO.md. Then summarize what changed and what is next.
```

## Recovering From An Interrupted Session

Use `RECOVERY_PROMPT.md`.

## Working In A Browser Chat Without File Access

Paste:
1. `PROJECT_CONTEXT.md`
2. `CURRENT_TASK.md`
3. The relevant slice of `DECISIONS.md`
4. Only the code section relevant to your question

The whole `index.html` is one file — paste just the function or section being discussed, not the whole thing.

## The One Rule That Matters Most

**Write things down before you stop.**

A 3-line session log entry takes 30 seconds and saves 10 minutes of context rebuilding at the start of the next session.
