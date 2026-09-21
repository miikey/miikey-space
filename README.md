# Miikey — deployment package

Current approved English single-page website with the lowercase `miikey_` wordmark, Geist Mono typography and blue underscore (`#3659dd`).

## Deployment

- **Publish directory:** `site/`
- **Build command:** none
- **Install command:** none
- **Runtime:** static HTML, CSS and fonts; no backend, API keys or JavaScript needed
- **GitHub Pages:** workflow supplied in `.github/workflows/pages.yml`

Read **[DEPLOY.md](DEPLOY.md)** for the deployment-agent handoff and custom-domain setup.

## Local preview

From this package’s root:

```sh
python3 -m http.server 8000 --directory site
```

Then open `http://localhost:8000/`.

## Files

```text
.github/workflows/pages.yml
DEPLOY.md
README.md
site/
  index.html
  .nojekyll
  native-mark.svg
  assets/
    site.css
    fonts.css
    inter-latin.woff2
    geist-mono.woff2
    inter-OFL.txt
    geist-OFL.txt
```

All local asset paths are relative. The page works at a custom domain root or a GitHub project Pages subpath. Fonts are included locally; retain their accompanying SIL Open Font License files.

Edit `site/index.html` for copy and `site/assets/site.css` for presentation. No generator is required. Historical design experiments and the previous hosting service’s configuration are intentionally excluded.
