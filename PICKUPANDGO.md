# Pick Up and Go

Handoff notes for whoever (human or AI session) picks this project up next.
**Read this first, then keep it current:** update the "Current state",
"Open items", and "Change log" sections whenever you change the project.

_Last updated: 2026-10-26_

---

## What this is

The public website for **SGX3 Fall Training 2026**, a free, 100% virtual
training program for undergraduates (HPC, AI/SI, Science Gateways, plus
professional development). Oct 19 – Dec 30, 2026, Mon & Wed 6–8 PM ET,
$500 stipend for selected participants.

- Live site: https://hackhpc.org/sgx3-fall-training-2026/
- Repo: https://github.com/HackHPC/sgx3-fall-training-2026 (branch `main`)
- Application form: https://forms.gle/UMbYaVC8EJu2Vsfu7

## Where to look

| Need | File |
|---|---|
| Program info (public-facing) | `README.md` |
| How the site is built, run, changed, deployed | `DEVELOPMENT.md` (detailed; read before editing) |
| Site settings, apply URL, SEO image | `_config.yml` |
| Home page content | `index.html` |
| Session Summaries list page (`/session-summaries/`) | `session-summaries.html` |
| One session summary per file | `_sessions/session-NN.md` (layout `_layouts/session.html`) |
| Resources page (`/resources/`) | `resources.html` (renders `_data/resources.yml`) |
| All resource links (name, url, description, group, session) | `_data/resources.yml` |
| Page shell / header / footer | `_layouts/default.html`, `_includes/header.html`, `_includes/footer.html` |
| All styles (color tokens in `:root`) | `assets/css/site.css` |
| Only JS: mobile menu | `assets/js/main.js` |

## How it works (30-second version)

- **Jekyll** site (home page + Session Summaries + Resources), built by **GitHub Pages** from `main` / root.
  Pushing to `main` deploys in ~1–2 minutes. No CI config, no CNAME
  (the `hackhpc.org` domain belongs to `HackHPC/hackhpc.github.io`).
- Served under `baseurl: /sgx3-fall-training-2026` — every internal link
  and asset must use `{{ '/path' | relative_url }}`.
- `sessions` collection in `_config.yml` → each `_sessions/*.md` renders at
  `/session-summaries/<name>/`; list page sorts by `session:` (newest first).
  How to add one: see "Add a session summary" in `DEVELOPMENT.md`.
- Resources page is generated from `_data/resources.yml` (grouped tables;
  stack into cards under 700px). "Shared in Session N" links to
  `/session-summaries/session-0N/`, so keep the `session-NN` file naming.
- Our stylesheet is `assets/css/site.css`, NOT `style.css`: the default
  `jekyll-theme-primer` (forced by `github-pages`) also renders
  `assets/css/style.css` and can overwrite ours depending on build order.
- Nav links use `{{ '/' | relative_url }}#section` so they work from subpages.
- Only plugin: `jekyll-seo-tag`. Gems via `github-pages` gem.
- Local dev needs **Ruby 3.3** (`.ruby-version` = 3.3.12; Ruby 4 is not
  supported by `github-pages`).

```bash
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve      # http://127.0.0.1:4000/sgx3-fall-training-2026/
JEKYLL_ENV=production bundle exec jekyll build   # sanity build
gh api repos/HackHPC/sgx3-fall-training-2026/pages/builds/latest -q '.status'
```

## Rules to keep

- **Every new link goes on the Resources page.** Whenever a link is added
  anywhere (a session summary, home page, etc.), also add it to
  `_data/resources.yml` with name, url, description, the right group, and
  `session:` if it came from a session. (Standing instruction from the user.)
- Only publish **confirmed** program details. No deadline, seat count,
  eligibility rules, sponsors, partners, or contact emails until the
  program team confirms them.
- Don't edit/redraw `assets/images/sgx3-logo.svg` (official logo).
- If Apply buttons come back (`.btn-apply` CSS is kept), use navy text on
  orange; never white-on-orange, and no orange text on light backgrounds.
- If `application_url` changes, regenerate `assets/images/apply-qr.svg`
  (command in `DEVELOPMENT.md`) and scan-test it.
- New files that shouldn't be published must be added to `exclude:` in
  `_config.yml` (README, DEVELOPMENT, PICKUPANDGO, CLAUDE are excluded).

## Current state (as of 2026-10-26)

- Site is live. `main` is in sync with `origin/main` after the 2026-10-26 push.
- Local production build passes on Ruby 3.3.12.
- Sections: Hero, About (`#about`), What You'll Learn (`#training`),
  Why Participate (`#benefits`), Program at a Glance (`#details`),
  Application (`#apply`: heading, blurb, application URL, QR code).
  NSF acknowledgment in footer.
- **Session Summaries** nav tab + list page + Session 1 summary (2026-10-19)
  added 2026-10-26.
- **Resources** nav tab + page added 2026-10-26; now 26 links in 6 groups
  (Session 1 + Session 2 directories, plus platforms named in Session 2).
- **Session 2 summary** (2026-10-21) added 2026-10-26 as `_sessions/session-02.md`.
- **Session 3 summary** added 2026-10-26 as `_sessions/session-03.md`; date
  assumed 2026-10-26 (next Monday after Session 2; not stated in the text).
- All of the 2026-10-26 work was committed and pushed to `main` on 2026-10-26
  (live on GitHub Pages).
- All **Apply Now buttons removed** (2026-10-26): header (desktop + mobile),
  hero, Program at a Glance, and `#apply` section. Still linking to the form:
  the URL + QR in `#apply` and the footer link "Apply to SGX3 Fall Training 2026".

## Open items / ideas

- **The program started Oct 19, 2026.** Apply Now buttons are gone, but the
  `#apply` section (URL + QR), footer apply link, README "How to Apply",
  OG image, and `DEVELOPMENT.md` (section table, pre-push checklist) still
  reference applying. Confirm whether to remove/replace those too, e.g. with
  an "in progress" / schedule page.
- **Session 1 summary names students** with class year, major, hometown, and
  high school, and attributes discussion opinions to them. The page is public
  once pushed; confirm with the program team that this is OK before pushing.
- Session 1 summary is user-supplied text; its claims (e.g. the Sept 29, 2026
  NSF "AI → SI" terminology change, cooling statistics) and the
  sciencegateways.org links in its resource table were not verified.
- **Student Deliverables Google Drive** link from Session 2 was deliberately
  NOT published (it holds student submissions; the page says "Shared with
  participants in Slack"). Only add it if the user explicitly confirms.
- **Session 2 links still missing URLs** ("Link shared in chat"): Abraham's
  GitHub portfolio and the Live Demo page. Add them to `session-02.md` and
  `_data/resources.yml` when the user provides them.
- **Replaced 3 broken (404) Session 1 links** with best-guess working pages;
  confirm with the user: SGX3 Student Programs →
  sciencegateways.org/education-training/student-focused; ADMI → admiusa.org;
  ORNL PCIP → orau.org/ornl/student-programs (also used for Session 2's
  "Zintellect ORNL PCIP" row). "ADMI Symposium" URL loads but lands on the
  generic sciencegateways.org Events page.
- Jeaime's GitHub Profile uses github.com/jeaimehp (from `gh api user`).
- Session 2 edits to user text: "nairpilot.org" → nairrpilot.org, "Texas
  Advanced Computer Center" → Computing, "Kimora / Qimora Mason" → Kimora
  Mason (matches Session 1); ASCII diagrams turned into tables.
- Session 3 was trimmed to ONLY the Linux "Technical Core" (user: that was
  the only thing covered). Removed from the pasted text: overview, SGX3
  framework, AI→SI pivot, student AI debate, cooling, MetaMuse, program
  milestones (Dec 1–3 site visit, Dec 7–11 Costa Rica hackathon, Dec 14
  portfolio presentations, early-2027 stipend), Charlie Nelson welcome, and
  the resource directory. Those milestones are unpublished; ask before
  adding them anywhere.
- Never add links to Google Drive deliverable folders (shared or per-student).
- Add Session 4+ summaries as they are provided.
- No session schedule, syllabus, or materials pages exist yet.
- Context outside the repo (parent folder `../`): branding assets,
  overview slides PDF, screenshots, transcripts, and an accepted-students
  spreadsheet. **Never commit participant data to this public repo.**

## Change log

Newest first. Add a line for every meaningful change.

- 2026-10-26 — Trimmed Session 3 to the Linux Technical Core only (new title,
  description; headings promoted).
- 2026-10-26 — Added Session 3 summary (ASCII diagrams → tables, commands →
  code blocks); added `.prose code`/`pre` styles; removed Charlie Nelson
  folder row per user.
- 2026-10-26 — Added Session 2 summary; added 14 links to `_data/resources.yml`
  (new "Training Modules" group); fixed 3 broken Session 1 links in both
  `session-01.md` and `resources.yml`.
- 2026-10-26 — Renamed `assets/css/style.css` → `site.css` (theme Primer's
  `style.css` was overwriting it during `jekyll serve` rebuilds).
- 2026-10-26 — Added Resources page: `_data/resources.yml`, `resources.html`,
  nav tab, table/card CSS. Standing rule: new links always go there too.
- 2026-10-26 — Added Session Summaries: `sessions` collection, `session-summaries.html`,
  `_layouts/session.html`, `_sessions/session-01.md`, nav tab (with `aria-current`),
  page/prose CSS; nav anchors now absolute to the home page; DEVELOPMENT.md updated.
- 2026-10-26 — Removed all Apply Now buttons (header, mobile header, hero,
  Program at a Glance, `#apply`) and their CSS; nav toggle now right-aligns
  itself on mobile.
- 2026-10-26 — Added `PICKUPANDGO.md` (this file) and `CLAUDE.md`
  pointer; excluded both from the Jekyll build.
- 2026-10-11 — Rewrote README with program info; added `DEVELOPMENT.md` (`cf6db5f`).
- 2026-10-11 — Added sunrise hero artwork (`43c1a0c`).
- 2026-10-11 — Added NSF logo + funding acknowledgment to footer (`c7ff16b`).
- 2026-10-11 — Built the Jekyll event site (`65a03fb`).
