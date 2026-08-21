# Testing the Astro double-nest fix (CLOUD-590)

This branch adds static assets that make the Astro 6/7 asset-serving bug (CLOUD-515)
directly observable, so you can compare a **buggy** builder against the **fixed**
`@webflow/app` package.

## The bug

Deployed at a **non-root mount** (e.g. `/app`), a fixed `@astrojs/cloudflare` adapter
nests the client under `dist/client/<mount>/`, and the old asset copy re-appends the
mount again → assets land at `assets/<mount>/<mount>/…` → served at `/<mount>/<mount>/…`
→ **404** at the URL the page references. The page still renders (SSR), but its CSS,
favicon, and images are broken.

> **Why `astro` is pinned to `6.4.8`.** The double-nest only triggers when the build
> actually nests the client under the mount, and that is astro-version-dependent:
> astro `6.1.4` builds a **flat** `dist/client/` (so the old copy lands it correctly —
> the bug does NOT reproduce), while `6.4.8`+ nests under `dist/client/<mount>/`. This
> branch pins `6.4.8` so the nesting path is exercised and the bug reproduces reliably.

## Assets in this branch

- `public/asset-check.txt` — plain-text marker at a known path (easy to `curl`).
- `public/mount-test.svg` — a check-mark image rendered on the homepage via the
  mount-aware `import.meta.env.BASE_URL`. Broken image = double-nested assets.
- `src/styles/global.css` (existing) — bundled into `_astro/*.css`; unstyled page = broken.

## How to test

Deploy at a **non-root mount** (e.g. `/app`) with the V2 engine (`COSMIC_BUILD_ENGINE=v2`),
twice:

### 1. Reproduce the bug — buggy builder (`@webflow/app@0.1.0-beta.6`, current main)

- Homepage loads but is **unstyled**, the check image is **broken**, favicon missing.
- `curl -i https://<host>/<mount>/asset-check.txt` → **404**
- `curl -i https://<host>/<mount>/<mount>/asset-check.txt` → **200** (proof of the double-nest)

### 2. Verify the fix — fixed builder (`@webflow/app@0.1.0-cloud590.0`, infra PR #7456)

- Homepage is **styled**, the check image **renders**, favicon shows.
- `curl -i https://<host>/<mount>/asset-check.txt` → **200**
- `curl -i https://<host>/<mount>/<mount>/asset-check.txt` → **404**

## Optional: also exercise the adapter pin

To test `ensureFixedCloudflareAdapter` too, pin a buggy adapter in `package.json`
(`"@astrojs/cloudflare": "13.2.0"`): the fixed builder force-upgrades it to `^13.3.1`
and warns; the buggy builder leaves it in place.
