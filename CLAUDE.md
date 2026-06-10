# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Project Overview

**Eats & Places** is a lightweight personal travel and food tracking web app delivered as a single `index.html` file. No build tools, no dependencies, no backend — all data persists in browser `localStorage`.

For full product context and design rationale, read [eats-places-handover.md](eats-places-handover.md). For development rules and constraints, read [AGENTS.md](AGENTS.md).

---

## Working with the Codebase

### Editing

- All code lives in `index.html`: HTML markup, CSS (in `<style>`), and JavaScript (in `<script>`).
- Edit directly with a text editor or use Claude Code's edit tools.
- No build step or compilation — changes are live once saved.

### Testing

- Open `index.html` in a web browser (desktop or mobile Safari) to test locally.
- For iPhone Safari, host on Vercel or Netlify and open from a Home Screen shortcut to ensure proper `localStorage` context.
- Use browser DevTools (Inspect → Application/Storage) to inspect or clear `localStorage` during testing.

### Deployment

- Keep the filename as `index.html` at repository root.
- Deploy to **Vercel** (user's preferred platform) or **Netlify Drop** (drag and drop).
- Vercel example: import the GitHub repo or drag `index.html` to vercel.com to generate a live URL.

---

## Architecture

### Data Model

All persistent data is stored in `localStorage` with three keys:

| Key | Type | Content |
|-----|------|---------|
| `ep-log-v1` | JSON array | Trip log entries: `{date, place, type, notes}` |
| `ep-togo-v1` | JSON array | To-go wishlist items: `{name, area, done}` |
| `ep-theme-v1` | String | Theme preference: `"light"` or `"dark"` |

### Design System

- **CSS Variables** at `:root` and `[data-theme="dark"]` control all spacing, colors, typography, shadows, transitions, and radius.
- **Light/Dark Mode**: toggle stored in `ep-theme-v1`, applied via `data-theme` attribute on `<html>`.
- **Safe Area Insets**: handled via CSS custom properties for iPhone notch/home bar (e.g., `env(safe-area-inset-bottom)`).
- **Responsive Typography**: uses CSS clamp() for fluid scaling across viewport sizes.

### Markup Structure

- Two-tab interface: **Trip Log** (page 1) and **To-Go List** (page 2).
- Sticky top bar with brand, theme toggle, and tab navigation.
- Tab content wrapped in `.page` containers (only `.page.active` displays).
- Tab count badges show pending (not done) to-go items.

### Key JavaScript Functions

Look for these patterns in the `<script>` block:

- **Tab switching**: update `.active` class on tabs and pages; sync count badge.
- **Form submission**: save entry, clear inputs, persist data to `localStorage`, show toast notification.
- **Delete**: remove item, update `localStorage`, refresh display.
- **Theme toggle**: toggle `data-theme`, save preference.
- **Initialization**: load `localStorage` on page load, pre-fill date input with today's date, hydrate DOM.

---

## Non-Obvious Rules

**Do not change without user request:**

- Storage keys `ep-log-v1`, `ep-togo-v1`, `ep-theme-v1` — used by deployed instances; renaming breaks existing data.
- Two fixed stay shortcuts (**Camili** and **Yagcilar**) — hardcoded, not editable. Tapping fills place name and switches type to "Stayed".
- Default trip log type to **Food** — matches primary use case (food exploration during travel).
- **Date and type persist after save** — allows fast repeat entry for the same day; only place and notes clear.
- **Newest day first** in timeline — most recent travel day always at top.
- **Pending items above completed** in to-go list — clear visual separation.
- **No sample data button**, **no sync**, **no PDF export**, **no external dependencies** — user explicitly requested these to be omitted.

---

## Design Constraints

- **Mobile-first** and optimized for iPhone Safari; all controls must hit 44px minimum tap target.
- **Offline-first**: app works entirely in the browser once loaded; no network requests.
- **Minimal and clean**: avoid framework-style abstractions; keep code direct and readable.
- **Safe area support**: padding and insets must account for iPhone notch/home bar.
- **Accessible**: meaningful labels, keyboard-navigable forms, sufficient color contrast.

---

## Deployment Notes

- **Primary target**: Vercel (user has an account).
- **Alternative**: Netlify Drop (app.netlify.com/drop — no account needed).
- On iOS, the app must be opened via **Home Screen shortcut** (not Files app) to preserve `localStorage` context across sessions.
- Vercel handles HTTPS, CDN, and custom domain support out of the box.

---

## When Resuming Development

1. Read the full context in [eats-places-handover.md](eats-places-handover.md) before making changes.
2. Note the fixed stay shortcuts (Camili, Yagcilar) and other intentional constraints listed there.
3. Keep changes to `index.html` unless updating project documentation.
4. After editing, test in a browser (desktop or mobile Safari) and verify data persistence works.
5. Commit changes and deploy to Vercel when ready.
