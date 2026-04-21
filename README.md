# Musa — marketing site

This repo hosts the public-facing site for **Musa**, an AI practice companion
for musicians. It's a tiny three-surface static site served off GitHub Pages:

| Surface        | Path        | Purpose                                                  |
| -------------- | ----------- | -------------------------------------------------------- |
| Landing page   | `/`         | Marketing home — features, demo, downloads, community    |
| Pitch deck     | `/pitch/`   | 18-slide investor/partner story (the original deck)      |
| Pilot signup   | `/signup/`  | Email capture backed by Supabase                         |

**Live site:** https://perice-pope.github.io/ai-music-companion-pitch/

## What's in here

- `index.html` — landing page (hero, features, demo, downloads, tutorials, docs, community, footer)
- `pitch/index.html` — the full 18-slide pitch deck, self-contained
- `signup/index.html` — pilot-program signup form backed by Supabase
- `.github/workflows/pages.yml` — auto-deploys every push to `main`

All three pages are single-file static HTML with inline CSS. No build step,
no framework, no bundler. The signup page pulls in `@supabase/supabase-js` from
an ESM CDN at runtime.

## Editing

```bash
# open any page directly
open index.html
open pitch/index.html
open signup/index.html

# or serve the whole site locally
python3 -m http.server 8000
# then visit http://localhost:8000/
```

Pushes to `main` auto-deploy to GitHub Pages via the workflow in
`.github/workflows/pages.yml`.

## Site structure

```
/                 — landing page (marketing home)
├── #features     — three-card feature grid
├── #demo         — demo video placeholder (YouTube, coming soon)
├── #download     — macOS / Windows / Linux cards ("coming soon")
├── #tutorials    — 3-card tutorial library (YouTube, coming soon)
├── #docs         — docs card (coming soon)
└── #community    — Discord + GitHub cards

/pitch/           — 18-slide pitch deck with keyboard navigation
/signup/          — pilot signup form, writes to Supabase
```

The landing page nav has a **Join the pilot** CTA in the top-right and a
final CTA section above the footer. Both link to `/signup/`.

## Signup backend (Supabase)

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
leaked, rotate it in the Supabase dashboard and update `signup/index.html` —
no other changes needed.

### Reading signups

Supabase dashboard → `musa` project → Table editor → `pilot_signups`. Or in
the SQL editor:

```sql
select created_at, email, name, role, instrument, notes
from pilot_signups
order by created_at desc;
```

## Placeholders to fill in

The landing page ships with honest "coming soon" labels on surfaces that
aren't ready yet. Swap these in as they materialize:

- **Demo video** (`index.html` `#demo` section) — replace the placeholder
  frame with a YouTube embed once the walkthrough is filmed.
- **Download buttons** (`#download` section) — swap the three "Coming soon"
  buttons for links to GitHub Releases (or hosted installers) per platform
  once beta 1.0 ships.
- **Tutorial cards** (`#tutorials` section) — replace the three `href="#"`
  placeholders with real YouTube URLs as videos publish.
- **Docs link** (`#docs` section) — point to `/docs/` (or an external docs
  host) once documentation is drafted.
- **Discord invite** (`#community` section) — replace the placeholder `href="#"`
  with the permanent invite URL once the server is created.
- **Custom domain** — once `musa.app` (or similar) is registered, add a
  `CNAME` file to the repo root with the bare domain.

## Roadmap

Shipped:

- Landing page with all sections (placeholders where needed)
- Pitch deck (18 slides, keyboard-navigable, print-friendly)
- Pilot signup form writing to Supabase with RLS

In flight / soon:

- Beta builds of the desktop app for macOS, Windows, Linux
- Demo video and first tutorial batch on YouTube
- Public Discord server
- `/docs/` with setup and instrument-profile reference

Later:

- Magic-link auth and a member area (gated downloads + practice dashboard)
- Custom domain
- Blog / devlog section under `/blog/`
