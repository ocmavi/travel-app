# Eats & Places — Project Handover

## Project Overview

This document is a full handover brief for continuing development of **Eats & Places**, a lightweight personal travel and food tracking web app. It is intended to be shared with Claude (or any AI assistant) to resume work with full context.

The app is a single self-contained HTML file with no build tools, no frameworks, no external dependencies, and no backend. All data is stored in the browser using `localStorage`.

---

## What This App Is

A simple personal daily tracker for two purposes:

1. **Trip Log** — record places visited, food spots tried, and overnight stays each day
2. **To-Go List** — a running wishlist of restaurants and places to visit, with tick-off functionality

The primary use case is **food exploration** (restaurants, cafes, local spots) during travel, with a secondary use for tracking daily movement and stays.

---

## Current State of the App

### File
- Filename: `index.html`
- Single HTML file — all CSS, JS, and markup are inline
- No external dependencies (uses `-apple-system` font stack, no CDN)
- Fully offline-capable once loaded in browser

### Tech Stack
- **HTML/CSS/JS** — vanilla only, no frameworks
- **localStorage** — permanent in-browser data persistence
- **Keys used:**
  - `ep-log-v1` — trip log entries
  - `ep-togo-v1` — to-go wishlist
  - `ep-theme-v1` — light/dark theme preference
- **Hosting target:** Vercel (user has account) or Netlify Drop

### Design System
- Custom CSS variables (Nexus-inspired warm palette)
- Light and dark mode with toggle, preference saved to localStorage
- Mobile-first layout, optimised for iPhone Safari
- Apple system font (`-apple-system`) for native iOS feel
- `safe-area-inset` padding for iPhone notch/home bar support
- `apple-mobile-web-app-capable` meta tag — can be added to iPhone Home Screen as a PWA-like shortcut

---

## Features Built

### Tab 1 — Trip Log

| Feature | Detail |
|---------|--------|
| Date input | Pre-filled with today's date on every load |
| Place input | Free text, autocorrect off |
| Quick Stay buttons | **Camili** and **Yagcilar** — tap to autofill place name and auto-select "Stayed" type |
| Entry types | 🍽️ Food (default), 📍 Visit, 🏠 Stayed, 📌 Upcoming |
| Notes field | Optional free text (dish name, rating, address, tip) |
| Save button | Saves entry, clears place + notes, keeps date and type for fast repeat entry |
| Timeline | Entries grouped by date, newest day first |
| Stats bar | Days tracked / Total places / Food spots |
| Delete | Per-entry delete button |
| Save toast | "Saved ✓" pill appears briefly after every save or delete |

### Tab 2 — To-Go List

| Feature | Detail |
|---------|--------|
| Add form | Name + optional area/city field |
| Enter key | Submits the add form |
| Tick off | Tap checkbox to mark as done (strikes through, fades) |
| Done section | Completed items separate below a divider |
| Clear done | Button to remove all completed items at once |
| Delete | Per-item delete button |
| Count badge | Tab shows count of pending (not done) items only |

---

## Intentional Design Decisions

- **No sample data button** — removed per user request
- **"Stayed" type has two fixed places** — Camili and Yagcilar are permanent quick-fill buttons, not editable in UI
- **Food is the default type** — matches primary use case (food exploration)
- **Date and type persist after save** — allows fast repeat entry for the same day
- **Newest day first** — most recent travel day always at top of timeline
- **No PDF export** — explicitly not required
- **No sync** — local device only, by design (simple, private, no account needed)

---

## Fixed Quick-Stay Places

The user always stays at one of two fixed locations. These are hardcoded as quick-fill buttons:

```
📍 Camili
📍 Yagcilar
```

Tapping either button:
1. Fills the place name field
2. Automatically switches the type to "🏠 Stayed"
3. Highlights the tapped button

**Do not make these editable** unless the user explicitly requests it.

---

## Deployment

### Target Platform
- **Vercel** (user has an existing account)
- Alternative: **Netlify Drop** (app.netlify.com/drop) — no account needed, drag and drop

### Deploy Steps
1. Go to vercel.com → Add New Project → import the GitHub repo or drag and drop `index.html`
2. Vercel generates a live URL (e.g. `https://eats-places.vercel.app`)
3. Open the URL on iPhone in Safari
4. Tap Share → Add to Home Screen

### iPhone Usage Rule
- Must be opened from the **Home Screen shortcut**, not from the Files app
- Opening from Home Screen ensures consistent `localStorage` context
- Local data persists across sessions as long as Safari storage is not cleared

---

## Known Issues / Limitations

| Issue | Status |
|-------|--------|
| Cannot open local HTML file in iPhone Safari via Files app | Resolved by hosting on Vercel/Netlify |
| localStorage not available in private/incognito mode | By design — user uses normal browsing |
| Data does not sync across devices | Intentional — single device use |
| No backup/export | Not yet requested |

---

## Possible Future Features (Not Yet Built)

These have not been requested but may come up:

- **Edit entry** — currently entries can only be deleted and re-added
- **Search / filter** — filter log by type or date range
- **JSON export / import** — backup and restore data
- **Notes expansion** — tap to expand long notes in the timeline
- **Rating field** — star or number rating for food spots
- **Multiple fixed stays** — if user adds more permanent home base locations

---

## How to Resume Development with Claude

When continuing work, paste this document into a new Claude conversation and attach the latest `index.html` file. Then describe what you want to change. Example prompt:

> "Here is my Eats & Places travel and food tracker handover doc, and the current HTML file is attached. I want to [describe the change]."

Claude can read the full HTML source and make targeted edits without breaking existing features.

---

## User Profile Context

- **Platform:** iPhone (primary daily use), Mac (file management and deployment)
- **Cloud storage:** iCloud Drive
- **Hosting:** Vercel account active
- **Technical level:** UX/Experience Designer with HTML/CSS knowledge — comfortable reviewing and understanding code
- **App style preference:** Clean, minimal, mobile-first, dark mode support, no heavy frameworks, no CDN dependencies
- **Primary goal:** Fast daily data entry on the go, especially logging food spots and restaurants

---

*Last updated: June 10, 2026*
