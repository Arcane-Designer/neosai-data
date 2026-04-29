# Neosai

A daily Japanese vocabulary system delivered via Claude Routines, with a dashboard for tracking progress and managing personal word lists.

## Architecture

- **Claude Routines** fire on schedule, generate each word fresh, and write to GitHub
- **`state.json`** — single source of truth. Tracks delivery history, characters covered, current week, user-added words.
- **`character-order.json`** — priority order for character-of-the-week selection (hiragana → katakana → kanji starter set)
- **Cloudflare Worker** — handles dashboard writes back to GitHub (no manual copy-paste)
- **Dashboard** at `arcanedesigner.com/neosai` — reads state, allows adding/editing personal words

## Schedule

| Day | Time | Content |
|-----|------|---------|
| Mon-Thu | 8:00 AM, 5:00 PM | Word of the day, reinforced in evening |
| Fri | 8:00 AM, 5:00 PM | Funword Friday, reinforced in evening |
| Sat | 11:00 AM | Weekly recap |
| Sun | 5:00 PM | Master recap (everything to date) |

Each weekday word contains the character of the week. The character changes every Monday; the routine picks the next from `character-order.json` that hasn't been used.

## Files

```
neosai-data/                    (private GitHub repo)
├── state.json                  ← live state, updated by routines
├── character-order.json        ← priority list, rarely edited
└── README.md
```

The dashboard (HTML/JS) lives in the `arcanedesigner.com` repo under `neosai/`.
