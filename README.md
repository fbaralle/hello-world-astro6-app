# hello-world-astro6-app

A minimal **Astro 6** starter deployed on [**Webflow Cloud**](https://webflow.com/cloud).

This is the vanilla variant — styled with a branded landing page and a few doc links. Uses Tailwind v4 via the Vite plugin.

> Looking for the variant with Cloudflare bindings (D1, R2, KV)?
> See [`hello-world-astro6-app-bindings`](https://github.com/Webflow-Examples/hello-world-astro6-app-bindings).

[![Deploy to Webflow](https://webflow.com/img/deploy-dark.svg)](https://webflow.com/dashboard/cloud/deploy?repo=https://github.com/Webflow-Examples/hello-world-astro6-app)

## Requirements

- Node **22.12+** (see `engines`).

## Quickstart

```bash
nvm use          # picks up required Node version
npm install
npm run dev
# → http://localhost:4321
```

## Deploy to Webflow Cloud

1. Fork this repo.
2. In your Webflow site, open **Apps → Webflow Cloud → Create new app** and select this repo.
3. Pick a mount path and click **Deploy**.

Full walkthrough: <https://developers.webflow.com/webflow-cloud/quickstart>.

## What's included

- Astro 6 (no framework islands)
- Tailwind CSS v4 via `@tailwindcss/vite`
- Branded landing page with Webflow Cloud doc links

## Customizing

The landing page lives in `src/pages/index.astro`. Styles are in
`src/styles/global.css` under the `wf-*` prefix.

## Learn more

- [Webflow Cloud docs](https://developers.webflow.com/webflow-cloud)
- [Astro on Webflow Cloud](https://developers.webflow.com/webflow-cloud/frameworks/astro)
- [Astro documentation](https://docs.astro.build)

---

Built with Astro · Deployed on Webflow Cloud.
