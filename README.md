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
- Rest timer feature has been removed.
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
- Google Drive sign-in using the Drive `appDataFolder` scope.
- Automatic Drive sync after sign-in, after local changes, when the app comes back online, and when the tab becomes visible.

## Google Drive Setup

To make Drive sync work for everyone, create one Google Cloud project for the app:

1. Enable the Google Drive API.
2. Configure the OAuth consent screen.
3. Create an OAuth Client ID with application type `Web application`.
4. Add `https://richhank.github.io` to Authorized JavaScript origins.
5. Paste the public Client ID into `GOOGLE_OAUTH_CLIENT_ID` near the top of `index.html`, then commit and push.

Every user opens the Drive screen, taps `Sign in with Google`, and approves app-specific Drive access. Their workout data is saved to their own Google Drive `appDataFolder`, separate from every other user. If `GOOGLE_OAUTH_CLIENT_ID` is still blank, the Drive screen shows an owner setup field so you can test with a Client ID before baking it into the hosted app.

## Notes

The app uses `https://www.googleapis.com/auth/drive.appdata`, which limits access to files this app creates in the hidden app data folder. It does not request full Drive file access.
