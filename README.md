# Neosai

A personal Japanese ledger: the words Nathan has met, and the characters he has marked as learned.

As of 2026-09-06 there are **no routines or automations**. Everything is manual, from the dashboard.

## Architecture

- **Dashboard** at `arcanedesigner.com/neosai` (source: `neosai/` in the `Arcane-Designer/main` repo, served by GitHub Pages). Two tabs: **Words** (add / edit / delete) and **Characters** (hiragana, katakana, kanji tiles that flip to show which of your words use them, with a learned toggle).
- **`state.json`** — single source of truth. `user_words` is the word list, `all_characters_learned` is the list of learned characters. Routine-era fields are kept empty for schema compatibility.
- **`character-order.json`** — the character inventory (hiragana, katakana, then Joyo kanji with grade and meaning) used to draw the Characters tab.
- **Cloudflare Worker** `neosai-worker` — reads and writes `state.json` on GitHub so the dashboard never needs a token in the browser.

## History

- 2026-04-29: system start (routine-delivered words).
- 2026-07-13: v3 reset (three funword routines a week).
- 2026-09-06: v4 reset to manual-only. Routines deleted, delivered words wiped, personal words kept. Pre-reset state is in git history (commit `ac4b7a3`).
