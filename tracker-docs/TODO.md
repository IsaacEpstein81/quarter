# 15-Min Tracker — Master Checklist

Last updated: 2026-05-23

---

## Core App (MVP)

- [x] 15-minute countdown ring timer
- [x] Ring color changes: purple → yellow → red as time runs out
- [x] Audio alarm — synthesized 3-note ding (C-E-G chord)
- [x] Vibration on alarm
- [x] Web push notification on alarm (with permission prompt)
- [x] Log entry modal — slides up from bottom on alarm
- [x] Modal shows time range (from – to)
- [x] Auto-focus textarea on modal open
- [x] Character count (200 max)
- [x] Save entry → closes modal, restarts timer
- [x] Skip entry → closes modal, restarts timer
- [x] Pause / Resume tracking
- [x] Log Now button — log manually without waiting for alarm
- [x] Today's log — timestamped entries in scrollable list
- [x] Delete individual entries
- [x] History tab — all past days, newest first
- [x] Expandable day cards in history
- [x] Time span shown per day (first entry → last entry)
- [x] Export CSV — all history in one file
- [x] iOS Share Sheet on mobile for export
- [x] Direct download on Mac/desktop for export
- [x] LocalStorage persistence per day
- [x] PWA installable (manifest + service worker)
- [x] Green blinking dot on Today tab while tracking

---

## Deployment

- [ ] Copy 3 files to a dedicated project folder
- [ ] Push to GitHub
- [ ] Deploy to Vercel
- [ ] Open on iPhone in Safari and add to home screen
- [ ] Enable push notifications on iPhone
- [ ] Confirm alarm fires correctly on iPhone

---

## Voice Input

- [ ] Tap-to-dictate button in the log entry modal
- [ ] Use Web Speech API (`SpeechRecognition`) — no backend needed
- [ ] Append transcribed text to textarea (don't replace, in case user typed something)
- [ ] Show visual indicator while listening
- [ ] Fallback: hide button if browser doesn't support Speech API

---

## AI Summary (In-App)

Phase 1 (manual — already possible):
- Export CSV → paste into Claude or ChatGPT → ask for summary

Phase 2 (in-app):
- [ ] "Summarize my day" button in History tab
- [ ] Send today's entries to Claude API
- [ ] Show formatted summary (time breakdown, focus areas, patterns)
- [ ] Requires Anthropic API key — decide whether to store in app settings or use a backend

---

## Cloud Sync

- [ ] Decide: anonymous device ID vs. full account (email / OTP)
- [ ] Set up Supabase project
- [ ] Define table schema (user_id, date, entries JSONB)
- [ ] Replace localStorage read/write with Supabase calls
- [ ] Handle offline gracefully — queue writes when offline, sync on reconnect
- [ ] Migrate existing localStorage data to Supabase on first sync

---

## Categories / Tags

- [ ] Define tag set (e.g. Deep Work, Admin, Personal, Health, Social, Break)
- [ ] Add tag picker to log entry modal
- [ ] Show tag color dot on each log entry
- [ ] Filter by tag in History
- [ ] Include tag column in CSV export
- [ ] Show tag breakdown in AI summary

---

## Configurable Interval

- [ ] Settings screen with interval selector (10 / 15 / 20 / 30 min)
- [ ] Persist selected interval in localStorage
- [ ] Restart timer with new interval when changed

---

## Weekly View

- [ ] Week-at-a-glance screen
- [ ] Show hours tracked per day as a bar chart or simple grid
- [ ] Click a day to jump to its entries in History

---

## Streaks / Consistency

- [ ] Track days with at least N entries as "active" days
- [ ] Show current streak and longest streak
- [ ] Simple visual on History screen

---

## Polish

- [ ] Swipe down to dismiss modal (touch gesture)
- [ ] Light mode support (`prefers-color-scheme: light`)
- [ ] Better empty state when History has no data
- [ ] Confirm before deleting an entry (or undo toast)
- [ ] Keyboard shortcut to open Log Now (desktop)
