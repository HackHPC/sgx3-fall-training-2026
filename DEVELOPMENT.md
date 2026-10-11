# Website Development Guide

This guide explains how the SGX3 Fall Training 2026 website works, how to run it on your own computer, and how changes get published. For information about the program itself, see the [README](README.md).

- **Live site:** https://hackhpc.org/sgx3-fall-training-2026/
- **Repository:** https://github.com/HackHPC/sgx3-fall-training-2026

---

## How the Page Works

### Overview

The site is a single web page built with [Jekyll](https://jekyllrb.com/), the static site generator that GitHub Pages runs. Jekyll combines a layout, a few reusable snippets, and the page content into one finished HTML file. There is no database, no server-side code, no front-end framework, and no tracking.

```text
_config.yml ──┐
              ├──► _layouts/default.html ──► _site/index.html (the finished page)
index.html ───┤        ├── _includes/header.html
              │        └── _includes/footer.html
assets/ ──────┘  (CSS, JavaScript, and images are copied as-is)
```

### Files

```text
_config.yml              Site settings: title, URLs, application link, social image
_layouts/default.html    Page shell: <head>, SEO tags, favicons, header, footer
_includes/header.html    SGX3 logo, navigation, Apply Now button, mobile menu toggle
_includes/footer.html    Footer links and the NSF funding acknowledgment
index.html               All page content, section by section
assets/css/style.css     All styles (colors and sizes are defined at the top in :root)
assets/js/main.js        The mobile menu toggle (the only JavaScript on the site)
assets/images/
  sgx3-logo.svg          Official SGX3 logo (do not edit or redraw)
  nsf-logo.svg           NSF logo for the funding acknowledgment
  hero-sunrise-*         Hero artwork: WebP at 800/1280/1983px + JPEG fallback
  apply-qr.svg           QR code that opens the application form
  og-image.png           1200×630 preview image shown when the link is shared
  favicon.svg, favicon-32.png, apple-touch-icon.png
Gemfile                  Ruby gems (the github-pages gem pins Jekyll and its plugins)
.ruby-version            Ruby version for local builds (3.3.12)
```

### Page Sections

`index.html` contains each section in order. The navigation links jump to these IDs:

| Section | ID | What it shows |
|---|---|---|
| Hero | — | Program name, tagline, dates, schedule, stipend, Apply Now and Explore the Program buttons |
| About the Program | `#about` | Program description and focus areas (HPC, AI, SI, Science Gateways) |
| What You'll Learn | `#training` | Three cards: Technical Skills, Professional Development, National Computing Resources |
| Why Participate? | `#benefits` | Seven participant outcomes |
| Program at a Glance | `#details` | Key program facts and the stipend note |
| Application | `#apply` | Final call to action, full application URL, and QR code |

### Key Settings in `_config.yml`

| Setting | Value | Purpose |
|---|---|---|
| `url` | `https://hackhpc.org` | Domain used for canonical and social-sharing links |
| `baseurl` | `/sgx3-fall-training-2026` | Subfolder the site lives in |
| `application_url` | `https://forms.gle/UMbYaVC8EJu2Vsfu7` | Used by **every** Apply Now button |
| `repository_url` | GitHub repository | Footer link |

Because the site lives in a subfolder, every internal link and asset path goes through Jekyll's `relative_url` filter, for example `{{ '/assets/css/style.css' | relative_url }}`. Keep that pattern when you add images or links, or they will break on the live site.

### Design System

Colors are CSS variables at the top of `assets/css/style.css`:

| Variable | Color | Used for |
|---|---|---|
| `--navy` | `#081D42` | Hero, application section, headings |
| `--blue` | `#0866DC` | Links, section labels, icons |
| `--orange` | `#F47722` | Apply Now buttons, accents |
| `--tint` | `#F1F6FC` | Alternating section backgrounds |

Accessibility notes:
- Apply Now buttons use **navy text on orange** (5.9:1 contrast). White text on orange does not meet WCAG AA.
- On light backgrounds, orange is only used for decoration (lines, bullets, borders), never for text.
- The hero artwork has a navy gradient over it so the white text stays readable.

### Responsive Behavior

| Screen width | Behavior |
|---|---|
| Wider than 920px | Full horizontal navigation; hero text on the left with the artwork filling the background |
| 920px and below | Navigation collapses behind a **Menu** button; Apply Now stays visible in the header |
| 820px and below | Hero artwork becomes a band above the text; key facts and cards stack in one column |
| 600px and below | Compact header (icon-only menu button, "Fall Training 2026" label hidden) |

### JavaScript

`assets/js/main.js` only controls the mobile menu. It opens and closes the menu, closes it when a link is selected or <kbd>Esc</kbd> is pressed, and keeps `aria-expanded` up to date for screen readers. If JavaScript is unavailable, the menu stays visible, so navigation always works.

Smooth scrolling is done in CSS and is turned off for visitors who have "reduce motion" enabled.

### SEO and Link Previews

The `jekyll-seo-tag` plugin (`{% seo %}` in the layout) generates the page title, meta description, canonical URL, Open Graph, and Twitter card tags. The page description is in the front matter at the top of `index.html`. The preview image is set under `defaults` in `_config.yml`.

---

## Running the Site Locally

### 1. Install the prerequisites

You need **Ruby 3.3** and **Bundler**.

> **Important:** The `github-pages` gem does not support Ruby 4.x. Use Ruby 3.3, which is what GitHub Pages runs. The `.ruby-version` file pins 3.3.12 for version managers like `rbenv` or `asdf`.

**macOS (with Homebrew and rbenv):**

```bash
brew install rbenv ruby-build
rbenv install 3.3.12
```

**Windows:** Install Ruby 3.3 from [RubyInstaller](https://rubyinstaller.org/) (choose the "with Devkit" version).

**Linux:** Use your package manager or `rbenv`, and make sure Ruby 3.3 is installed.

Then install Bundler:

```bash
gem install bundler
```

### 2. Get the code

```bash
git clone https://github.com/HackHPC/sgx3-fall-training-2026.git
cd sgx3-fall-training-2026
ruby -v    # should report 3.3.x
```

### 3. Install the dependencies

```bash
bundle config set --local path vendor/bundle   # keeps gems inside the project folder
bundle install
```

### 4. Start the local server

```bash
bundle exec jekyll serve
```

Open **http://127.0.0.1:4000/sgx3-fall-training-2026/** in your browser.

> Include the `/sgx3-fall-training-2026/` path. Visiting only `http://127.0.0.1:4000/` shows a blank or 404 page because of the `baseurl` setting.

The server rebuilds the site automatically when you save a file; refresh the browser to see the change. Changes to `_config.yml` are the exception: stop the server (<kbd>Ctrl</kbd>+<kbd>C</kbd>) and start it again.

To build the site without running a server (output goes to `_site/`):

```bash
JEKYLL_ENV=production bundle exec jekyll build
```

### Troubleshooting

| Problem | Fix |
|---|---|
| `undefined method 'tainted?'` | You are on Ruby 3.2 or newer with an old `github-pages` version. Delete `Gemfile.lock` and run `bundle install` again on Ruby 3.3. |
| `github-pages ... requires Ruby >= 2.6, < 4.0` | You are on Ruby 4. Switch to Ruby 3.3 (`rbenv local 3.3.12`). |
| `cannot load such file -- webrick` | Run `bundle install`; `webrick` is listed in the `Gemfile`. |
| Styles or images are missing | Check that you are using the `/sgx3-fall-training-2026/` URL and that new paths use `relative_url`. |
| `Address already in use` | Another server is running. Stop it, or use `bundle exec jekyll serve --port 4001`. |

---

## Making Common Changes

**Edit program text:** Change the section in `index.html`. Also update the README and the description in the front matter of `index.html` if they repeat the same information.

**Change the application link:**
1. Update `application_url` in `_config.yml`.
2. Regenerate the QR code (see below).

**Regenerate the QR code** (requires [`qrencode`](https://fukuchi.org/works/qrencode/), e.g. `brew install qrencode`):

```bash
qrencode -t SVG -l M -m 2 --rle -o assets/images/apply-qr.svg "https://forms.gle/UMbYaVC8EJu2Vsfu7"
```

Scan the new code with a phone before you commit, and make sure it opens the right form.

**Replace the hero artwork:** Export the new image at 800, 1280, and full width as WebP, plus a 1280px JPEG, using the same `hero-sunrise-*` file names. To adjust the crop, change `object-position` on `.hero-art img` in `style.css`.

**Change colors:** Edit the variables in `:root` at the top of `style.css`, then check text contrast with a tool like the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).

### Content guidelines

Only publish confirmed program details. Don't add an application deadline, number of positions, stipend eligibility rules, sponsors, partners, or contact addresses until the program team confirms them.

### Before you push

- [ ] `bundle exec jekyll build` runs with no errors
- [ ] The page looks right on a desktop and on a phone-width window
- [ ] Every Apply Now button opens `https://forms.gle/UMbYaVC8EJu2Vsfu7`
- [ ] The navigation links jump to the correct sections
- [ ] New images have meaningful `alt` text, or `alt=""` if they are decorative

---

## Deployment

Publishing is automatic. GitHub Pages builds the site from the **`main` branch, root folder**, so changes pushed to `main` appear on the live site, usually within a minute or two.

```bash
git add -A
git commit -m "Describe your change"
git push origin main
```

To check the build, open the repository's **Actions** tab on GitHub or run:

```bash
gh api repos/HackHPC/sgx3-fall-training-2026/pages/builds/latest -q '.status'
```

### How the site gets its URL

The HackHPC organization site ([HackHPC/hackhpc.github.io](https://github.com/HackHPC/hackhpc.github.io)) owns the custom domain `hackhpc.org`. GitHub Pages serves every project repository in the organization under that domain at `/<repository-name>/`, so this repository is published at `https://hackhpc.org/sgx3-fall-training-2026/` automatically.

- **Do not add a `CNAME` file** to this repository. The domain belongs to the organization site.
- Keep `url` and `baseurl` in `_config.yml` as they are, so canonical and social-sharing links stay correct.
- Enforcing HTTPS for `hackhpc.org` is configured in the `hackhpc.github.io` repository's Pages settings, not in this repository.
