# Recovery Prompt

Use this if a prior session ended unexpectedly before the end-of-session prompt was run.

```text
The previous session ended unexpectedly.

Please:
- read tracker-docs/README.md
- read tracker-docs/CURRENT_TASK.md
- read tracker-docs/DECISIONS.md
- read tracker-docs/TODO.md
- read tracker-docs/SESSION_LOG.md
- read index.html (the full app source)

Then:
1. Tell me what was likely in progress based on the docs and code.
2. Tell me what looks done but may not be documented yet.
3. Recommend the safest next step.
4. Refresh CURRENT_TASK.md and SESSION_LOG.md so the docs match the code.
5. Continue only after summarizing the recovery state.
```

## What Usually Survives

- All saved code in `index.html`, `manifest.json`, `sw.js`
- All markdown docs in `tracker-docs/`
- All localStorage data on the user's device

## What Is Lost After An Interrupted Session

- Any unsaved edits to files
- The reasoning from the chat that was never written to a file
- Timer state (always resets to 15:00 on page load — this is by design)
