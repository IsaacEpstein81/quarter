# Decisions

## 2026-05-23

### Pure Static Site — No Framework

Decision:
Build as a single `index.html` with no npm, no build step, no framework.

Reason:
The user wanted something deployable to the phone immediately. A single file is the fastest path: open in any browser, deploy to Vercel in one command, add to home screen from Safari. Nothing to install or compile.

### LocalStorage Per-Day Keys

Decision:
Store each day's log as a separate localStorage entry under the key `tracker_log_v1_YYYY-MM-DD`.

Reason:
Keeps days cleanly separated. Scanning all day keys is easy (prefix match). Makes it simple to load just today without touching the rest. Easy to export or migrate later.

### CSV As The Export Format

Decision:
Export all historical data as a single CSV file with columns: Date, Day, Time, Notes.

Reason:
CSV is universally readable. Easy to paste into Claude or ChatGPT for an AI summary. Easy to open in Numbers, Excel, or Google Sheets. Simpler than JSON for non-technical use.

### Share Sheet On Mobile, Direct Download On Desktop

Decision:
Use `navigator.share()` with a File object on touch devices (`navigator.maxTouchPoints > 0`). Fall back to a standard `<a download>` link on desktop.

Reason:
iOS Safari does not download files directly to a folder — it opens a Share Sheet instead. The Share Sheet lets users save to Files, AirDrop to Mac, email to themselves, etc. Desktop browsers support standard downloads natively. The touch detection (`maxTouchPoints`) distinguishes iPhone from Mac Safari, which also supports the Share API but shouldn't use it since desktop downloads work better there.

### Synthesized Audio — No Audio File

Decision:
Generate the alarm sound using the Web Audio API (3-note C-E-G sine wave chord).

Reason:
No file to host or cache. Works offline immediately. Sounds clean and intentional. Avoids any licensing concerns.

### Service Worker Cache Version Must Be Bumped Manually

Decision:
When deploying a new version of the app, increment the cache string in `sw.js` (e.g. `tracker-v1` → `tracker-v2`).

Reason:
The service worker caches `index.html`. If the cache version is not bumped, returning users get the old HTML even after a Vercel deploy. Bumping the version triggers the `activate` event to delete the old cache.

### Timer State Is Not Persisted

Decision:
Timer state (secondsLeft, isRunning) lives only in memory. Closing or refreshing the tab resets it to 15:00.

Reason:
The user starts tracking fresh each morning by tapping Start. Persisting timer state across tab closes adds complexity and edge cases (what if the tab was closed for 3 hours?). Saved entries in localStorage are always safe.

### No Backend For MVP

Decision:
Ship with localStorage only. No backend, no database, no auth.

Reason:
The user wanted something on their phone the same day. A backend means accounts, hosting, API keys, and latency. localStorage is instant, works offline, and is plenty for one person's daily log. Add Supabase later when cloud sync becomes a real need.

### Vercel For Hosting

Decision:
Deploy as a static site on Vercel.

Reason:
Zero config for static files. Free tier. Instant deploys from git push. Global CDN. HTTPS out of the box, which is required for service workers and the Share API.
