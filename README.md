# Workout Log

Static, no-framework workout logger hosted on GitHub Pages.

Live app: https://richhank.github.io/workout-log/

## Current Architecture

- Static SPA in `index.html`.
- Permanent dark UI.
- PWA shell with `manifest.json`, install icons, and `sw.js`.
- Offline-first browser storage using IndexedDB with localStorage fallback.
- Full-state JSON export/import is the canonical round-trip format.
- CSV export/import is for set rows only.
- Gist sync fallback stores one JSON blob in a GitHub Gist and merges records by `updated_at`.

## Implemented In This Slice

- PWA shell and offline cache.
- Dark-only palette, no theme toggle.
- Exercise database/editor.
- Program/day/block data model.
- Add exercise and swap exercise flows.
- Basic plan editor with drag reorder, rest-day type, and new-plan wizard.
- Rest timer based on `Date.now()` deltas with vibrate/audio notification and mute-ready settings storage.
- CSV schema:

```csv
date,exercise,set_number,reps,weight_lb,rpe,notes
2026-05-03,Back Squat,1,5,225,7.5,felt fast
```

- CSV import preview with added/changed/unchanged/errored counts.
- JSON backup/import.
- PR trendline canvas view using Epley e1RM.
- Daily workout notes and editable session duration tracking.
- Exercise-level duration and average-rest summaries.
- Strength standards comparison using bundled starter data in `strength-standards.json`.
- Gist sync fallback screen.

## Supabase TODO

The requested primary sync path needs a Supabase project URL, anon key, auth configuration, and table policies. Once those exist, wire these tables:

- `profiles`
- `exercises`
- `programs`
- `program_days`
- `program_blocks`
- `sessions`
- `sets`

The local state model now mirrors that shape closely enough to map records into those tables.

## Notes

The Gist fallback asks for a GitHub PAT with `gist` scope only. The app does not remember the token unless the user explicitly selects that option.
