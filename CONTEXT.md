# CONTEXT — hello-world-astro6-app

Orientation for contributors to this **Astro 6** Hello World example for
[Webflow Cloud](https://developers.webflow.com/webflow-cloud). Keep this file
current when structure or workflows change.

## What this is

A minimal, branded **Hello, world** page built with **Astro 6** and deployed on
Cloudflare Workers via Webflow Cloud. This is the **vanilla** variant
(no bindings — UI only).

The page shows a Webflow brand hero, gradient logo, and curated doc cards
pointing at the Webflow Cloud documentation.

## Stack

- Framework: **Astro 6** (requires Node ≥ 22.12)
- Styling: Tailwind v4 (`@tailwindcss/vite`) + `wf-*` brand tokens
  (see `src/styles/global.css`)
- Deploy target: Cloudflare Workers via **Webflow Cloud**

## Repo layout

```
src/
  pages/index.astro          ← page content, hero, DOC_LINKS
  layouts/Layout.astro       ← root layout (head, meta)
  components/
    WebflowLogo.astro
    DocCard.astro
  styles/global.css          ← Tailwind v4 + .wf-* design tokens
astro.config.mjs
package.json
```

## Running locally

```bash
npm install
npm run dev
```

Requires Node 22.12+ (set in `.nvmrc`).

## Building

```bash
npm run build
```

Build output lands in `dist/`.

## Editing the UI

- **Page content (hero, CTAs, doc cards):** `src/pages/index.astro`
- **Doc card list:** search for `DOC_LINKS` in `src/pages/index.astro`
- **Layout / `<head>`:** `src/layouts/Layout.astro`
- **Brand tokens and `.wf-*` styles:** `src/styles/global.css`

## Deploying to Webflow Cloud

1. Push this repo to GitHub.
2. In your Webflow Cloud project, connect the repo and pick a mount path
   (e.g. `/my-app`). The app runs under any prefix.
3. Webflow Cloud builds with `npm run build` on deploy.

See [Deployments](https://developers.webflow.com/webflow-cloud/deployments)
and [Environments](https://developers.webflow.com/webflow-cloud/environments).

## Contributing

- Keep the **Webflow brand tone**: blue gradient (`#4353FF` → `#146EF5`), dark
  background, minimal copy. Reuse the existing `.wf-*` CSS tokens.
- This is a Hello World. Do **not** add extra pages, client-state libraries,
  or UI kits. Small and readable beats clever.
- Run `npm run build` before opening a PR.
- Keep **cross-app parity**: if you change shared copy or doc links, update
  the sibling `hello-world-*-app[-bindings]` apps too.

## Related docs

- [Webflow Cloud overview](https://developers.webflow.com/webflow-cloud)
- [Getting started](https://developers.webflow.com/webflow-cloud/getting-started)
- [Storing data (SQLite, KV, R2)](https://developers.webflow.com/webflow-cloud/storing-data/overview)
- [Environments](https://developers.webflow.com/webflow-cloud/environments)
- [Deployments](https://developers.webflow.com/webflow-cloud/deployments)
- [Configuration](https://developers.webflow.com/webflow-cloud/environment/configuration)
- [Node.js compatibility](https://developers.webflow.com/webflow-cloud/environment/nodejs-compatibility)
- [Limits](https://developers.webflow.com/webflow-cloud/limits)
