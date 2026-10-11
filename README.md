# SGX3 Fall Training 2026

Event website for **SGX3 Fall Training 2026**, a 100% virtual training program for undergraduate students in research computing, HPC, AI/SI, and Science Gateways.

- **Live site:** https://hackhpc.org/sgx3-fall-training-2026/
- **Apply:** https://forms.gle/UMbYaVC8EJu2Vsfu7

The site is a single-page [Jekyll](https://jekyllrb.com/) site built for GitHub Pages. It has no frameworks or tracking scripts, and uses a few lines of JavaScript for the mobile menu.

## Project structure

```text
_config.yml              Site settings (title, URLs, application link, SEO image)
_layouts/default.html    Page shell: <head>, SEO tags, header, footer
_includes/header.html    Logo + navigation
_includes/footer.html    Footer
index.html               All page sections (hero, about, training, benefits, details, apply)
assets/css/style.css     All styles; design tokens are at the top in :root
assets/js/main.js        Mobile navigation toggle
assets/images/
  sgx3-logo.svg          Official SGX3 logo (do not edit or redraw)
  apply-qr.svg           QR code for the application URL
  og-image.png           1200×630 social sharing image
  favicon.svg, favicon-32.png, apple-touch-icon.png
```

The application URL is set once, as `application_url` in `_config.yml`, and every **Apply Now** button uses it. If the URL ever changes, update `_config.yml` and regenerate the QR code (see below).

## Local development

Requirements: Ruby 3.3 (pinned in `.ruby-version`; the `github-pages` gem does not yet support Ruby 4) and Bundler.

```bash
bundle config set --local path vendor/bundle   # optional: keep gems in the project
bundle install
bundle exec jekyll serve
```

Then open http://127.0.0.1:4000/sgx3-fall-training-2026/. Note the subpath: the site uses `baseurl: /sgx3-fall-training-2026`, so all internal links and assets go through Jekyll's `relative_url` filter.

To build without serving:

```bash
JEKYLL_ENV=production bundle exec jekyll build   # output in _site/
```

### Regenerating the QR code

```bash
qrencode -t SVG -l M -m 2 --rle -o assets/images/apply-qr.svg "https://forms.gle/UMbYaVC8EJu2Vsfu7"
```

Scan the result (or decode it with a QR library) to confirm it opens the exact application URL before you commit.

## Deployment

Deployment is automatic. GitHub Pages builds this repository from the **`main` branch, root folder** (classic Pages build), so pushing to `main` publishes the site.

How the URL works: the HackHPC organization site ([HackHPC/hackhpc.github.io](https://github.com/HackHPC/hackhpc.github.io)) has the custom domain `hackhpc.org`. GitHub Pages serves every project repository in the organization under that domain at `/<repository-name>/`, so this repository appears at `https://hackhpc.org/sgx3-fall-training-2026/` without any extra configuration.

- Do **not** add a `CNAME` file to this repository. The custom domain belongs to the organization site.
- Keep `url: "https://hackhpc.org"` and `baseurl: "/sgx3-fall-training-2026"` in `_config.yml` so canonical and Open Graph URLs are correct.

## Content guidelines

Only publish confirmed program details. Don't add an application deadline, number of positions, stipend eligibility rules, sponsors, partners, or contact addresses until the program team confirms them.
