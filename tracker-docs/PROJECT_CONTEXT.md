# Project Context

## Product

**15-Min Tracker** is a mobile-first web app (PWA) for tracking what you do all day in 15-minute increments.

Core loop:
- User starts tracking at the beginning of their day
- Every 15 minutes an alarm dings and vibrates
- User types a few words about what they did in the last 15 minutes
- Entries are saved with timestamps and visible in a scrollable log
- At the end of the day, user exports a CSV and can run an AI summary

The goal is frictionless time awareness — not a productivity system, just an honest log.

## Current Stack

- **Pure static site** — one HTML file, no framework, no build step
- **PWA** — installable from Safari to iPhone home screen via manifest + service worker
- **localStorage** — data stored per-day in the browser; persists across reloads
- **Web Audio API** — synthesized 3-note ding alarm, no audio file needed
- **Vibration API** — haptic pulse on alarm
- **Web Notifications API** — optional lock-screen alerts
- **Web Share API** — iOS share sheet for CSV export (falls back to download on desktop)
- **Deployed on Vercel** — static hosting, zero config

## App Files

```text
index.html      — entire app (UI, logic, styles)
manifest.json   — PWA install metadata
sw.js           — service worker (offline cache)
```

## What Is Already Built

- 15-minute countdown ring timer (color changes: purple → yellow → red)
- Audio ding (C-E-G chord) on alarm
- Vibration pattern on alarm
- Web push notification prompt and alert on alarm
- Log entry modal — slides up from bottom, shows time range, auto-focuses input
- Pause / Resume tracking
- "Log Now" button to log manually at any time
- Today's log — timestamped entries, deletable
- History tab — browse all past days, expandable day cards, time span shown
- Export CSV — iOS Share Sheet on mobile, direct download on Mac/desktop
- LocalStorage persistence (per-day key: `tracker_log_v1_YYYY-MM-DD`)
- PWA installable (manifest + service worker)
- Green blinking dot on Today tab when tracking is active

## Planned Features (not built yet)

- Voice input — tap to dictate instead of type
- AI summary — end-of-day analysis of how time was spent
- Cloud sync — replace localStorage with Supabase so data survives cache clears and works across devices
- Categories / tags — optional color-coded labels per entry
- Weekly summary view
- Streaks and consistency tracking
