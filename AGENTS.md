# Travel App Agent Guide

Use this workspace as a tiny, static, single-file web app. The functional source of truth is [index.html](index.html), and the handover context lives in [eats-places-handover.md](eats-places-handover.md).

## Project Shape

- Treat the app as plain HTML, CSS, and vanilla JavaScript only.
- There is no build step, package manager, backend, or shared data store.
- All persistent data lives in browser `localStorage`.
- Keep changes self-contained in `index.html` unless you are updating project instructions.

## Non-Obvious Rules

- Preserve the storage keys `ep-log-v1`, `ep-togo-v1`, and `ep-theme-v1`.
- Keep the two fixed stay shortcuts, Camili and Yagcilar, hardcoded and non-editable.
- Default the trip log type to Food and keep date/type state after saving for fast repeat entry.
- Keep newest log days first and pending to-go items above completed ones.
- Do not add sample data, sync, PDF export, or external dependencies unless the user explicitly asks.

## UI / UX Constraints

- Keep the app mobile-first and iPhone Safari friendly.
- Preserve safe-area handling, the theme toggle, and the current offline-first behavior.
- Keep the interface clean and minimal; avoid framework-style abstractions for a one-file app.
- Maintain accessible controls and keyboard submit behavior where already present.

## Deployment Notes

- For deployment, keep the app entry file named `index.html` at repository root.
- If you need the full product context before editing, read [eats-places-handover.md](eats-places-handover.md) first.
