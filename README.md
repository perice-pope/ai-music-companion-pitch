# AI Music Companion — Pitch Deck

This repo hosts the public-facing pitch deck for **AI Music Companion**, a desktop practice tool for musicians.

**Live site:** https://perice-pope.github.io/ai-music-companion-pitch/

## What's in here

- `index.html` — the full slide deck (self-contained, no build step)
- `signup/index.html` — pilot-program signup landing page backed by Supabase

## Editing

The deck is a single HTML file with inline CSS and vanilla JS. Open it locally:

```bash
open index.html
```

Pushes to `main` auto-deploy to GitHub Pages via the workflow in `.github/workflows/pages.yml`.

## Signup page

Slide 18's **Join Us** CTA links to [`/signup/`](./signup/index.html), a static
landing page that writes pilot signups directly into Supabase.

**Live URL:** https://perice-pope.github.io/ai-music-companion-pitch/signup/

### Supabase backend

- **Project:** `musa` (ref `msptnffhkcgqwbzesfyz`, region `us-west-2`) under
  the `perice-pope's Org` organization
- **Table:** `public.pilot_signups`
  - `id uuid`, `email text` (unique, case-insensitive), `name`, `instrument`,
    `role` (student / teacher / studio / other), `notes`, `source`
    (defaults to `pitch-deck`), `user_agent`, `created_at`
- **RLS:** enabled. Anon role can `INSERT` only — no reads, updates, or
  deletes from the browser. Admins read signups via the Supabase dashboard
  (or the service-role key server-side).

The page uses the project's **publishable** anon key, which is safe to ship
client-side because RLS is what actually gates access. If the key is ever
compromised or leaked, rotate it in the Supabase dashboard and update
`signup/index.html` — no other changes needed.

### What's shipped vs. still to build

Shipped:

- Email + role + instrument capture into `pilot_signups`
- Case-insensitive duplicate-email handling (shows "you're already on the list")
- Graceful failure messaging with a mailto fallback

Still to build (tracked via issues on this repo):

- Magic-link auth and a member area (downloads + tutorials) — currently
  signups are just a mailing list; there is no login flow yet
- Desktop app download links (gated or ungated — decision pending)
- Tutorial library
- Custom domain (e.g. `musa.app`) so early signups don't bookmark the
  `github.io` URL

### Local testing

Open `signup/index.html` directly in a browser, or serve the repo root with
any static server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/signup/
```

Submissions from localhost go to the live Supabase project, so use a test
email (and clean it up in the dashboard afterward) unless you want to be in
your own pilot cohort.
