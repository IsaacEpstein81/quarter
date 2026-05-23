# MVP Execution Plan

## Current State

The core app is built and ready to deploy. It works as a daily tracking tool right now.

---

## Phase 1 — Deploy And Use (Now)

Objective: get the app on the phone and start collecting real data.

Steps:
1. Copy `index.html`, `manifest.json`, `sw.js` to a new project folder
2. Create a GitHub repo and push
3. Connect to Vercel — zero config needed, it auto-detects a static site
4. Open the Vercel URL in Safari on iPhone
5. Share → Add to Home Screen
6. Enable notifications when prompted
7. Use it for 1–2 weeks before adding features

Why wait before adding features:
Real usage will reveal what actually matters. The list of planned features is already long — daily use will show which ones are worth building.

---

## Phase 2 — Voice Input

Objective: reduce friction of the log entry step.

Why this first:
The log entry modal is the highest-friction moment. Voice input removes the need to type and keeps the 15-minute rhythm from feeling like a chore.

Approach:
- Web Speech API — browser-native, no backend or API key needed
- Works in Safari on iOS 14.5+
- Add a mic button inside the modal textarea
- Transcribe and append to the text field
- Takes ~1 day to build

---

## Phase 3 — Manual AI Summary (Already Possible)

Objective: let the user analyze their day without building any AI infrastructure.

How it works right now:
1. Tap Export CSV in the History tab
2. AirDrop to Mac (or save to Files)
3. Paste into Claude or ChatGPT
4. Ask: "Analyze how I spent my time today and summarize the patterns"

This is already usable. No code needed.

Build an in-app version only after using the manual flow enough to know what the ideal summary format looks like.

---

## Phase 4 — Cloud Sync

Objective: make data durable and device-independent.

Trigger to start:
- localStorage is cleared accidentally and data is lost, OR
- user wants to see their data on multiple devices

Approach:
- Supabase free tier — Postgres, simple REST API, no backend needed from the client
- Anonymous device ID stored in localStorage as the user identifier (no account required for V1)
- Each day's log is a row: `(device_id, date, entries JSONB)`
- Migrate existing localStorage data on first sync
- Keep localStorage as a local cache; Supabase as the source of truth

---

## Phase 5 — In-App AI Summary

Objective: one-tap end-of-day summary without leaving the app.

Approach:
- Add "Summarize my day" button in History tab
- Call Claude API directly from the browser (API key stored in a settings screen)
- Or proxy through a lightweight serverless function on Vercel to hide the key
- Display the summary as formatted text below the day's entries

Build this after Phase 4 (cloud sync) so the summary can span multiple days if needed.

---

## Phase 6 — Categories / Tags

Objective: make exports and summaries more structured and useful.

Approach:
- Fixed tag set initially (Deep Work, Admin, Personal, Health, Social, Break)
- Single tap to apply a tag in the modal
- Tags stored in the entry object alongside `text`
- Show as color dots in the log
- Include in CSV export
- Feed into AI summary for time-by-category breakdown

---

## What To Skip For Now

- Configurable interval — 15 minutes works; tweak later if real usage shows a different cadence is better
- Streaks — nice but not core; add after the data model is solid
- Native app — the PWA is good enough for one user; don't build a React Native app until there are multiple users who need push notifications that work reliably in background
