# atarist-public-floppy-database-web

Browsable website of the images downloadable with the SidecarTridge Multi-device.

**Live:** https://ataristpublicfloppydb.sidecartridge.com/

A single static page that reproduces the "Public Floppy Database" browser from the device's
on-board UI (`browser_home.shtml` in `md-browser`), hosted publicly so anyone can explore the
catalog without a device attached. It reads the public catalog
(`https://ataristdb.sidecartridge.com/db/*.csv`) and links each entry straight to its
downloadable `.ST` image.

## Stack

Plain static page — no build step. Alpine.js, Pure.css, and Font Awesome load from CDNs;
`index.html`, `styles.css`, and `favicon.png` are the only local files.

## Run locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000/
```

## Deploy

Pushing to `main` publishes to GitHub Pages via `.github/workflows/deploy.yml` (no build; the
repo root is uploaded as-is). The site is served over HTTPS on the custom domain in `CNAME`
(`ataristpublicfloppydb.sidecartridge.com`). In the repository settings, Pages → Build and
deployment → Source is **GitHub Actions**.

## SEO

`index.html` carries a keyword-aware `<title>` and meta description, a canonical link, Open
Graph and Twitter Card tags (preview image: the SidecarTridge logo), and JSON-LD structured
data (`WebSite` / `Organization` / `CollectionPage`). Mentions of the SidecarTridge
Multi-device link to its
[product page](https://sidecartridge.com/products/sidecartridge-multidevice-atari-st/).

## Notes

The catalog host `ataristdb.sidecartridge.com` serves `db/*.csv` over HTTPS — required because
GitHub Pages is HTTPS-only and browsers block http subresource fetches as mixed content.

## Backlog

Development is tracked in `docs/epics/` (a local-only, git-ignored backlog; run
`./docs/epics/cockpit.sh` to regenerate `docs/epics/STATUS.md`).
