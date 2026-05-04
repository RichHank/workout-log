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
- Google Drive sync stores one JSON blob in each user's hidden Drive app data folder and merges records by `updated_at`.

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
- Google Drive sync screen using the Drive `appDataFolder` scope.

## Google Drive Setup

To make Drive sync work for everyone, create one Google Cloud project for the app:

1. Enable the Google Drive API.
2. Configure the OAuth consent screen.
3. Create an OAuth Client ID with application type `Web application`.
4. Add `https://richhank.github.io` to Authorized JavaScript origins.
5. Paste the Client ID into the app's Drive screen.

Every user clicks `Connect Google Drive` and approves app-specific Drive access. Their workout data is saved to their own Google Drive `appDataFolder`, separate from every other user.

## Notes

The app uses `https://www.googleapis.com/auth/drive.appdata`, which limits access to files this app creates in the hidden app data folder. It does not request full Drive file access.
