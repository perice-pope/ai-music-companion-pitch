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
| `AI_Music_Companion_Platform_Strategy_v3.docx` | Platform-strategy writeup that accompanies the deck. Same vintage. |

## A note on public visibility

This repo is **public** because GitHub Pages on free-tier accounts requires it. Anything placed here — even inside `drafts/` — is world-readable. If something in a strategy doc is sensitive (pricing, partner lists, financials), either redact before committing, or keep the file in the private main repo (`ai-music-companion`) and only promote the public-safe pitch deck here.
