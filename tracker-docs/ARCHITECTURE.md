# Architecture

## File Map

```text
15min-tracker/
  index.html       — everything: layout, styles, all JavaScript logic
  manifest.json    — PWA name, icons, display mode, theme color
  sw.js            — service worker: caches app files, handles notification clicks
  tracker-docs/    — project memory (optional: can live in Hormozi/ instead)
```

## index.html Structure

### CSS (inside `<style>`)

CSS custom properties (`--bg`, `--accent`, `--surface`, etc.) control the entire color theme.

Key layout sections:
- `#app` — full-height flex column container
- `header` — title + date
- `#notif-banner` — yellow nudge to enable push notifications (hidden by default)
- `.view` — swappable content panels (Today / History)
- `#bottom-nav` — two-tab nav (Today / History)
- `#modal-overlay` + `#modal` — log entry sheet, slides up from bottom

### JavaScript Sections

```
State variables
  INTERVAL, secondsLeft, isRunning, tickInterval
  sessionStart, lastLogTime, audioCtx, currentTab

Timer logic
  toggleTimer() → startTimer() / stopTimer()
  tick() → counts down, calls onAlarm() at zero
  onAlarm() → plays sound, vibrates, sends notification, opens modal

Ring animation
  updateRing(fraction) → sets stroke-dashoffset + stroke color

Audio
  getAudioCtx() → lazy AudioContext init (required by iOS)
  playDing() → 3-note sine wave chord (C5, E5, G5)

Notifications
  checkNotifPermission() → shows banner if not yet granted
  sendNotification() → fires Web Notification on alarm

Modal
  openModal() → sets time range label, clears input, slides up
  saveEntry() → writes to localStorage, re-renders log, restarts timer
  skipEntry() → advances lastLogTime, closes modal, restarts timer

Storage
  todayKey() → "YYYY-MM-DD" string
  loadDayLog(dateKey) → parse from localStorage
  saveDayLog(dateKey, log) → serialize to localStorage
  getAllDayKeys() → scan all localStorage keys with our prefix

Rendering
  renderTodayLog() → rebuilds #log-list from today's entries
  renderHistory() → builds day cards in #history-list

Export
  exportData() → builds CSV, uses Share API on touch devices,
                  falls back to <a download> on desktop

Tab switching
  switchTab('today' | 'history')

Helpers
  formatTime(Date) → "8:32am"
  formatDateLabel(dateKey) → "Fri, May 22"
  escHtml(str) → basic XSS sanitization
  showToast(msg) → brief pill notification at bottom of screen
```

## Data Format

Each day's log is stored in localStorage under the key `tracker_log_v1_YYYY-MM-DD`.

The value is a JSON array of entry objects, newest first:

```json
[
  {
    "id": 1716381120000,
    "from": "2026-05-22T08:17:00.000Z",
    "to": "2026-05-22T08:32:00.000Z",
    "text": "morning coffee + reading"
  }
]
```

## Export Format (CSV)

```
Date,Day,Time,Notes
2026-05-22,Friday,8:32am,"morning coffee + reading"
2026-05-22,Friday,8:47am,"emails and Slack"
```

All historical days are included in one file, oldest entries first within each day, newest days first in the file.

## PWA / Service Worker

`manifest.json` declares the app as a PWA with standalone display mode and dark theme color.

`sw.js` caches `index.html`, `manifest.json` on install and serves from cache on fetch. Cache version is bumped manually (`tracker-v1`, `tracker-v2`, etc.) to force updates.

**Important:** When deploying a new version, bump the cache version string in `sw.js` or users will get stale HTML from the service worker cache.

## Where State Lives

| Data | Storage |
|------|---------|
| Today's entries | `localStorage` keyed by date |
| Past days | `localStorage` keyed by date |
| Timer state | In-memory JS variables (lost on page close) |
| Last log time | In-memory (lost on page close) |

This means: **closing the browser tab resets the timer to 15:00.** Entries already saved are safe. The timer state is not persisted — by design for now, since the user taps Start when they wake up.
