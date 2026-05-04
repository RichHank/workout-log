# Workout Log

Phone-first workout logger for the Upper/Lower split in `index.html`.

## Free Hosting Path

1. Create a public GitHub repository, for example `workout-log`.
2. Upload or push these files to the repository root:
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
   - `icon.svg`
   - `.nojekyll`
3. In GitHub, open `Settings -> Pages`.
4. Set `Build and deployment` to `Deploy from a branch`.
5. Choose `main` and `/root`, then save.
6. Open `https://YOUR-GITHUB-USERNAME.github.io/workout-log/`.
7. On iPhone Safari, tap Share, then Add to Home Screen.

## Storage

The app stores workout entries in IndexedDB first, with a localStorage fallback copy. It also has:

- CSV export for sending weekly logs to Claude.
- JSON backup for restoring the app data later.
- JSON import that merges backed-up sets back into the app.

Local browser storage is still device/browser storage. It can be cleared if the user deletes site data, uses private browsing, or resets the phone. The JSON backup is the free recovery path.
