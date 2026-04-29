# Neosai — Captain's Japanese Learning System

A daily Japanese vocabulary system delivered via Claude routines, with a dashboard for browsing words and managing personal lists.

## Architecture

- **Claude Routines** fire on a schedule and post notifications with the day's content
- **`state.json`** — the brain. Tracks what's been delivered, the current week, characters learned. The routines read and update this.
- **`curriculum.json`** — the pre-built word bank. 26 weeks of hiragana-foundation vocabulary. Captain doesn't read this directly (no spoilers).
- **`user-lists.json`** — Captain's manual additions: words already known (so the system skips them) and words learned outside the system.
- **`dashboard/`** — the static web UI hosted at arcanedesigner.com/neosai. Reads everything via raw GitHub URLs.

## Schedule

| Day | Times | Content |
|-----|-------|---------|
| Mon-Thu | 8:00 AM, 5:00 PM | Same word twice — full lesson AM, reinforcement PM |
| Fri | 8:00 AM, 5:00 PM | Funword Friday |
| Sat | 11:00 AM | Weekly recap (5 words + character of the week) |
| Sun | 5:00 PM | Master recap of all words and characters to date |

## Files reference

```
neosai-data/
├── state.json              # Live state, updated by routines
├── curriculum.json         # 26-week word bank, locked
├── user-lists.json         # Captain's manual lists
└── dashboard/
    ├── index.html
    └── dashboard.js
```

## Updating user lists

The dashboard is read-only. To add words to your "known" or "custom" lists:
1. Open the dashboard, go to **Manage Lists**
2. Add the entries via the forms
3. Click **Copy to clipboard** in the export zone
4. Paste into `user-lists.json` in this repo and commit

## Extending the curriculum

After 26 weeks, run `build_curriculum.py` to add more weeks. The format is documented in that script.
