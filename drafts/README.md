# Drafts

Work-in-progress pitch materials that aren't yet live. The served site (`https://perice-pope.github.io/ai-music-companion-pitch/`) always renders the repo-root `index.html`. Nothing in this folder ships to the public site.

## Promotion workflow

When a draft is ready to go live:

1. Back up the current `index.html` if you want to keep it: e.g. `mv index.html drafts/pitch-deck-v1.html`
2. Copy the new draft into place: `cp drafts/pitch-deck-v2.html index.html`
3. Commit, push. GitHub Pages auto-deploys.

## Files in this folder

| File | Notes |
|------|-------|
| `pitch-deck-v2.html` | Rebrand to "Musa" + revised narrative. Drafted 2026-04-19. Not yet promoted. |

## Public visibility rule

This repo is **public** because GitHub Pages on free tier requires it. Anything here — even inside `drafts/` — is world-readable.

**Strategy docs, financials, partner lists, pricing decks — don't commit them here.** They live in the private main repo (`perice-pope/ai-music-companion`). The repo's `.gitignore` explicitly excludes `*Platform_Strategy*.docx` and `*internal*` files as a safety net in case of a copy-paste slip.
