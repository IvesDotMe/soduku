# Sudoku

Single-file React Sudoku, packaged as an installable, offline-capable web app (PWA). Same themes and
layout language as the Spider Solitaire app (`../spider-solitaire`); the two share the theme setting.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole game (React via `React.createElement`, no build step) plus PWA meta tags and service-worker registration |
| `manifest.webmanifest` | Name, icons, standalone display |
| `sw.js` | Service worker: precaches the app shell; caches Google Fonts as they load |
| `vendor/react*.js` | React 18.3.1 UMD, vendored |
| `icons/` | Home-screen icons |

## Install on iPhone

Same as Spider: host over HTTPS (GitHub Pages: Settings → Pages → deploy `main` from `/ (root)`), open the
URL in Safari, play once so the cache fills, Share → Add to Home Screen.

## Game notes

- Levels by number of givens: Flash 52, Easy 42, Medium 34, Hard 28, Expert 24. Every puzzle is generated
  on the device (backtracking fill in a crypto-random order, then clues removed while a solution counter
  confirms the puzzle still has exactly one solution). Generation takes ~0.1–0.3 s.
- Play: tap a cell then a digit (or type 1–9, arrows to move, Backspace to erase, N toggles notes, H hint,
  Ctrl+Z undo). Wrong digits turn red and count as mistakes. Placing a digit clears that note from its
  row, column and box. Completing a row/column/box pops. The pad shows how many of each digit remain.
- Score: each correct digit earns 120 × level multiplier (1/2/3/5/8), decaying over 20 minutes to 25 %;
  a mistake costs 100 × multiplier, a hint 150 × multiplier; finishing adds a time bonus
  (2 × multiplier per second under 30 minutes).
- Storage (`localStorage`): `sudoku-save-v1` (game + undo history), `sudoku-stats-v1` (played/won per
  level, best score/time, streaks), `spider-solitaire-skin` (theme, shared with Spider).
