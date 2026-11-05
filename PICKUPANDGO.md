# Pick Up and Go

Handoff notes for whoever (human or AI session) picks this project up next.
**Read this first, then keep it current:** update the "Current state",
"Open items", and "Change log" sections whenever you change the project.

_Last updated: 2026-11-04_

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
  stack into cards under 700px). "Shared in Session N" links to that session's
  summary when one exists, and is plain text when it doesn't.
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

## Current state (as of 2026-11-04)

- Site is live. The 2026-11-04 session rewrite below was committed and pushed to
  `main` on 2026-11-04. The "confirm" items in Open items were still unanswered
  at push time, so that content is public as written.
- Sections: Hero, About (`#about`), What You'll Learn (`#training`),
  Why Participate (`#benefits`), Program at a Glance (`#details`),
  Application (`#apply`: heading, blurb, application URL, QR code).
  NSF acknowledgment in footer.
- **Session articles are being rewritten** from text the user pastes in, one
  session at a time. Old Sessions 1–3 removed 2026-11-04 (recoverable from git
  at `aa7b3c6`). New `session-01.md` through `session-05.md` are in; later
  sessions pending.
- **Resources** nav tab + page; old links were kept.
- All **Apply Now buttons removed** (2026-10-26): header (desktop + mobile),
  hero, Program at a Glance, and `#apply` section. Still linking to the form:
  the URL + QR in `#apply` and the footer link "Apply to SGX3 Fall Training 2026".

## Open items / ideas

- **The program started Oct 19, 2026.** Apply Now buttons are gone, but the
  `#apply` section (URL + QR), footer apply link, README "How to Apply",
  OG image, and `DEVELOPMENT.md` (section table, pre-push checklist) still
  reference applying. Confirm whether to remove/replace those too, e.g. with
  an "in progress" / schedule page.
- **Slack invite link deliberately NOT published.** The user's new Session 1
  text includes the live workspace invite; on this public site anyone could
  join with it. The page says "Invite shared directly with participants". Only
  add it if the user explicitly confirms.
- New Session 1 is user-supplied text. Edits made: citation markers removed,
  `nairpilot.org` → nairrpilot.org, event site URL `http` → `https`, ORNL PCIP
  renamed "Pathways to Computing Internship Program" (per the Zintellect page;
  the text said "Post-Master's / Undergraduate"), "program, virtual onboarding"
  → "program, virtually onboarding". Its claims (AI → SI terminology, AWS token
  evaluation, 400 projects / 44 states, 1 billion Muse tokens) were not verified.
- **New Sessions 2 and 3 publish the NSF site visit and Costa Rica Hackathon
  (Dec 7–11)**, as in the user's text. The site visit dates conflict: Session 2
  says Dec 2–3, Session 3 says Dec 1–3. Confirm the date and that both are OK to
  make public before pushing.
- New Sessions 2 and 3 name students (module roles, one student's portfolio, and
  Charlie Nelson joining the cohort), as in the user's text. Confirm with the
  program team before pushing.
- New Session 3 edits to user text: Drive folder URL withheld ("Shared directly
  with participants"); Charlie Nelson's student folder row removed (it's a
  personal Drive folder, and the user had this row removed from the old Session 3).
  The old Session 3 also left out the Charlie Nelson welcome and the milestones;
  the new text includes both, so they were kept. Its claims were not verified.
- New Session 2 edits to user text: citation markers removed, Drive folder URL
  withheld ("Shared directly with participants"), ORNL PCIP renamed as in
  Session 1, LinkedIn URL simplified to the main company page. Its claims were
  not verified.
- **Resources entries with no matching new article were kept** (e.g. Slack setup
  video, GitHub Pages Quickstart, ADMI, training module links). Review them once
  the new articles are in.
- New Session 4 edits to user text: "[suspicious link removed]" in the body →
  Buffer (inferred from the resource table; confirm), Slack invite and channel
  URLs withheld, "Charlie" → Charlie Nelson (matches Session 3), citation-free.
  It also lists workshop attendees by name, including Destiny Hackett. Its claims
  were not verified.
- New Session 5 edits to user text: Drive and Slack channel URLs withheld, fixed
  broken bold around `learntools`. It names Omnibond as an example of a company
  expecting AI agent use; confirm that's OK to publish. Its claims were not
  verified.
- Other milestones from the old Session 3 text (Dec 14 portfolio presentations,
  early-2027 stipend) are unpublished; ask before adding them.
- Never add links to Google Drive deliverable folders (shared or per-student).
- Add new Session 6+ summaries as they are provided. Transcripts for Sessions
  1–3 and 5 (`transcript-11-2.txt`) are in `../transcripts/`.
- No session schedule, syllabus, or materials pages exist yet.
- Context outside the repo (parent folder `../`): branding assets,
  overview slides PDF, screenshots, transcripts, and an accepted-students
  spreadsheet. **Never commit participant data to this public repo.**

## Change log

Newest first. Add a line for every meaningful change.

- 2026-11-04 — Added new Session 5 from user text (no new public links; Kaggle
  Python was already on Resources).
- 2026-11-04 — Added new Session 4 from user text; Resources: added Buffer and
  Perplexity AI.
- 2026-11-04 — Added new Session 3 from user text (no new public links; Bandit
  was already on Resources).
- 2026-11-04 — Added new Session 2 from user text; Resources: added Abraham's
  GitHub Portfolio and Jeaime Powell's Live Demo Web Page.
- 2026-11-04 — Removed old Session 1–3 articles; added new Session 1 from user
  text; Resources: added GitHub, LinkedIn, ADMI 2026 Teams, Muse AI join, swapped
  in real ADMI 2026 Symposium and Zintellect PCIP URLs; "Shared in Session N" is
  now plain text when that session has no article.
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
