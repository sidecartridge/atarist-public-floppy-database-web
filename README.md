# atarist-public-floppy-database-web

Browsable website of the images downloadable with the SidecarTridge Multi-device.

This is a single static page that reproduces the "Public Floppy Database" browser from
the device's on-board UI (`browser_home.shtml` in `md-browser`), but hosted publicly so
anyone can explore the catalog without a device attached. It reads the same public
catalog (`https://ataristdb.sidecartridge.com/db/*.csv`) and links each entry straight to
its downloadable image.

## Stack

Plain static page — no build step. Alpine.js, Pure.css, and Font Awesome load from CDNs;
`index.html`, `styles.css`, and `favicon.png` are the only local files.

## Run locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000/
```

## Deploy

Pushing to `main` publishes to GitHub Pages via `.github/workflows/deploy.yml` (no build;
the repo root is uploaded as-is). In the repository settings, set **Pages → Build and
deployment → Source** to **GitHub Actions** once.

## Requirement: HTTPS catalog host

GitHub Pages is served over HTTPS, and browsers block a background `fetch()` to an `http://`
URL as mixed content. The catalog host `ataristdb.sidecartridge.com` must therefore serve
the `db/*.csv` files over **HTTPS** for the catalog to load on the deployed site. Until then
the page renders but shows an empty catalog.

## Backlog

Development is tracked in `docs/epics/` (a local-only, git-ignored backlog; run
`./docs/epics/cockpit.sh` to regenerate `docs/epics/STATUS.md`).
