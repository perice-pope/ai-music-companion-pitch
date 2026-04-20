# AI Music Companion — Pitch Deck

This repo hosts the public-facing pitch deck for **AI Music Companion**, a desktop practice tool for musicians.

**Live site:** https://perice-pope.github.io/ai-music-companion-pitch/

## What's in here

- `index.html` — the full slide deck (self-contained, no build step)

## Editing

The deck is a single HTML file with inline CSS and vanilla JS. Open it locally:

```bash
open index.html
```

Pushes to `main` auto-deploy to GitHub Pages via the workflow in `.github/workflows/pages.yml`.

## Roadmap — signup landing page

Slide 18's "Join Us" CTA currently points to `#signup` as a placeholder. The plan
is to ship a real signup page at `/signup` on this same GitHub Pages site so we
keep one repo and one URL.

**Planned flow:**

1. Visitor clicks **Join Us** on slide 18 → lands on `/signup`
2. Signs up (email + instrument + role: student / teacher / studio)
3. Redirected to a member area with:
   - Desktop app download links (macOS / Windows)
   - Tutorial library (getting started, per-instrument walkthroughs)
   - Link to their practice dashboard once the app is installed

**Backend:** Supabase (free tier to start) for:

- Auth (magic-link email signup)
- `users` table: email, instrument, role, signup date, pilot cohort
- `downloads` table: which build + version each user pulled
- Later: `practice_sessions` synced from the desktop app

**Hosting:** GitHub Pages for now (static HTML + Supabase JS client from CDN).
If we outgrow Pages or need server-side rendering, migrate to Vercel or
Cloudflare Pages and point a custom domain at it.

**Open questions (decide before building):**

- Custom domain? (e.g. `musa.app`, `joinmusa.com`) — pick one before launch so
  early signups don't bookmark the `github.io` URL.
- Do teachers/studios get a different onboarding than individual students?
- Do we gate downloads behind signup, or let anyone download and only gate the
  cloud/sync features?

Track progress in issues on this repo tagged `signup-page`.
